# Kafka Internals, Scalability & Performance

Kafka ~ immutable commit log

### Kafka production challenges
- Frequent consumers rebalances
    - Frequent rebalances are usually caused because it is taking too long for the consumer to process batches. This happens because the consumer is processing the batch for a long time (and heartbeats are not being sent) and therefore the brokers think that consumer was lost and they start re-balancing.
    - Suggest to create smaller batches by reducing the value of ```max.partition.fetch.bytes``` or extend/increase heartbeat intervals by increasing the value of ```heartbeat.interval.ms```.

Kafka has implemented "Incremental Cooperative Rebalancing". So now there is no need for all consumers to stop the processing ("stop the world event") to rebalance work in group, when new consumer appears in group or some consumer goes offline.

- https://stackoverflow.com/questions/56647442/kafka-keeps-rebalancing-consumers
- https://stackoverflow.com/questions/71615472/kafka-commit-during-rebalancing

#### Kafka Streams

In-Stream Analytics (In our case it is limited to Trends) 
- Active SDDCs Count
- Active Users Count
- Latency Trends
- Anomaly Detection - Abnormal change in trends - Using Moving Average algorithms.

KTable is localized in-memory store, used groupy and aggregate events, can be configured to use with ROCKS_DB by default.

https://stackoverflow.com/questions/59628222/apache-kafka-implementing-a-ktable

### How Kafka Nodes and zookeeper will communicate with each other?

Apache Kafka uses Zookeeper to,
- Select a controller
- Maintain cluster membership
- Stores configurations such as list of topics, metadata for partitions and brokers

In order to remain part of the Kafka cluster, each broker has to send keep-alive to Zookeeper in regular intervals. This is something every Zookeeper client does by default. If the broker doesn't heartbeat Zookeeper every zookeeper.session.timeout.ms milliseconds (6000 by default), Zookeeper will assume the broker is dead. This will cause leader election for all partitions that had a leader on that broker. If this broker happened to be the controller, you will also see a new controller elected.

Source: https://stackoverflow.com/questions/54013250/how-kafka-nodes-and-zookeeper-will-communicate-with-each-other

#### What is Difference between broker-list and bootstrap servers?

--broker-list as it is now deprecated.

Now for both producer and consumer we have to use --bootstrap-server

#### Will Consumers connect to Zookeeper?

From v0.9 onwards, consumer has no zookeeper dependency and does not connect to zookeeper at all.

Consumer connects to a Kafka broker directly. Consumer offsets are stored in specific topic named __consumer_offsets.

### Kafka NO Longer Requires ZooKeeper (In future)

Until now, Apache ZooKeeper was used by Kafka as a metadata store. Metadata for partitions and brokers were stored to the ZooKeeper quorum that was also responsible for Kafka Controller election.

In upcoming release v2.8.0, ZooKeeper can be replaced by an internal _**Raft quorum of controllers**_. When Kafka Raft Metadata mode is enabled, Kafka will store its metadata and configurations into a topic called @metadata. This internal topic is managed by the internal quorum and replicated across the cluster. The nodes of the cluster can now serve as brokers, controllers or both (called combined nodes).
    https://towardsdatascience.com/kafka-no-longer-requires-zookeeper-ebfbf3862104 

### Where kafka stores metadata on zookeeper? (which path?)

By default, Kafka uses a number of paths in zookeeper:
- /brokers: Contains alive brokers as well as topics configuration, assignments and current ISRs (In-Syn Replicas)
    - /brokers/ids/[brokerId]
    - /brokers/topics/[topic]
    - /brokers/topics/[topic]/partitions/[partitionId]/state
- /controller: This ZNode is owned by the current controller in the Kafka cluster
- Consumer registration: /consumers/[groupId]/ids/[consumerId]
- Consumer owner: /consumers/[groupId]/owners/[topic]/[partitionId] -> string (consumerId)
- Consumer offset: /consumers/[groupId]/offsets/[topic]/[partitionId] -> long (offset)
- /admin: This contains delete topic requests
- /config: This contains overriden configs for brokers, quotas
    - /config/topics/[topic_name]

### Explan role of Kafka Controller?

Kafka controller is a thread that runs inside only one broker in a Kafka cluster i.e. If we have a cluster of N brokers then there will be only one broker that is the controller.

It is like a brain for the cluster so that the cluster functions in a smooth and resilient way.

Whenever a Kafka Cluster is spun up, the brokers will first create a session with the zookeeper and the brokers will try to create an ephemeral node “/controller” inside the zookeeper. The broker that will be able to successfully create the “/controller” node will become the controller.

The rest of the brokers will create a watch on this “/controller” node. As soon as the controller goes down or its session with the zookeeper is lost then this znode will be deleted and the rest of the brokers will be notified, and a new controller will be elected again.

In a Kafka cluster, one of the brokers serves as the controller, which is responsible for managing the states of partitions and replicas and for performing administrative tasks like reassigning partitions. At any given time there is only one controller broker in your cluster.

**_Transaction log is a Kafka Topic_**, it comes with the associated durability guarantees.

### Producer Example

Source: https://www.conduktor.io/kafka/complete-kafka-producer-with-java
```
ProducerRecord<String, String> producerRecord = new ProducerRecord<>(topic, key, value);

// send data - asynchronous
producer.send(producerRecord, new Callback() {
    public void onCompletion(RecordMetadata recordMetadata, Exception e) {
        // executes every time a record is successfully sent or an exception is thrown
        if (e == null) {
            // the record was successfully sent
            log.info("Received new metadata. \n" +
                "Topic:" + recordMetadata.topic() + "\n" +
                "Key:" + producerRecord.key() + "\n" +
                "Partition: " + recordMetadata.partition() + "\n" +
                "Offset: " + recordMetadata.offset() + "\n" +
                "Timestamp: " + recordMetadata.timestamp());
```

--bootstrap-server parameter occurs only for consumer. On the other side, --broker-list is on parameter list only for producer.

--broker-list
    - a full list of servers, if any missing producer may not work
    - related to producer commands

--bootstrap-servers
    - one is enough to discover all others
    - related to consumer commands
    - Zookeeper involved

### Topic & Partition Strategy

- Topics by product & tenant-group classfication
- Partitions count is driven by tenant-group classification

### Java Producer with Keys

When Kafka publishes a keyed message, the message is deterministically mapped to a partition based on the hash of the key. This provides a guarantee that messages with the same key are always routed to the same partition, which can be important for some applications. Remember that messages within a partition are always delivered in order to the consumer.

Keys become useful when a user wants to introduce ordering and ensure the messages that share the same key end up in the same partition.

Batching messages enables a Kafka producer to increase its throughput. Reducing the number of network requests the producer makes in order to send data will improve the performance of the system.

There are two parameters to configure on the Kafka producer that control message batching, and understanding these is key to optimising throughput. 
- batch.size - Upper bound batch size
- linger.ms - The maximum time to wait to reach batch size

### Consumer Example

https://www.conduktor.io/kafka/complete-kafka-consumer-with-java

### Tell me about Metadata requests in Kafka producer

The first time the producer makes a metadata request is when it connects to the bootstrap servers that you set in the client configuration. Of course, it can be just one broker or more but not necessarily all the brokers in the cluster (so the metadata request is not for each broker). In this way, the producer gets information about where are the topics that it wants to send messages. During its life, more metadata requests can be done when it receives an error connecting to the broker leader for the partition it's writing, in this case, it needs to know which broker is the new leader for connecting to it (if not connected yet for other topics) and starting to send.
https://stackoverflow.com/questions/56794122/metadata-requests-in-kafka-producer

### Consumers partition allcoation

:star::star::star https://developer.confluent.io/learn-kafka/architecture/consumer-group-protocol/

https://medium.com/lydtech-consulting/kafka-consumer-group-rebalance-1-of-2-7a3e00aa3bb4

A consumer belongs to a consumer group. Within the consumer group, consumers are assigned topic partitions from which to consume. Group membership is managed on the broker side, and partition assignment is managed on the client side.

Group Coordinator manages the consumer group and the consumers, is a Kafka component that lives on the broker side. It will make one consumer the lead, and this will be responsible for computing the topic partition assignments. These are returned to the Group Coordinator which then assigns the partitions to the consumers.

Given a single application instance, with a consumer with a group.id of ‘foo’ listening to a particular topic, and that topic has six partitions, then the consumer will poll for messages across all six partitions.

Now a second instance of the application is started. This therefore starts a second consumer instance with the same group.id of ‘foo’. The second consumer instance sends a JoinGroup request to the Group Coordinator, and the partitions are reassigned across the consumer group to spread the load. With two members in the consumer group, three partitions are assigned to each consumer instance.

#### Consumer Group Coordinator Vs. Consumer Group Leader
https://stackoverflow.com/questions/42015158/what-is-the-difference-in-kafka-between-a-consumer-group-coordinator-and-a-consu

### Is having a Consumer Group mandatory in Kafka?

Yes, it is mandatory to specify Kafka which consumer would belong to which consumer group. If you do not set the consumer group id in your app, you will get an exception. If you start a consumer to consume from a topic using the Kafka CLI command, then a new random consumer group is created with the name console-consumer-<some_random_number> and the consumer automatically falls under this consumer group.
    
https://medium.com/javarevisited/kafka-partitions-and-consumer-groups-in-6-mins-9e0e336c6c00
    

### Message Delivery Guarantees by Kafka?

Three different Message Delivery Guarantee types are supported by Kafka.

- Exactly once: **Despite broker failures or producer retries**, Kafka guarantees that every message will be stored only once, without duplications or data loss
- At-Least Once: Every message will always be saved in Kafka at least once, according to this rule. There is no chance of message loss, but if the producer tries again after the message has already been persisted, the message may be duplicated.
- At most Once: Every message in Kafka is only stored once, at most. If the producer doesn’t retry on failures, messages could be lost.

Source: https://hevodata.com/blog/kafka-exactly-once-semantics/#intro
        
### Idempotent Producer?

Idempotency is the second name of Kafka Exactly Once Semantics. To stop processing a message multiple times, it must be persisted to Kafka topic only once. During initialization, a unique ID gets assigned to the producer, which is called producer ID or PID.

PID and a sequence number are bundled together with the message and sent to the broker. As the sequence number starts from zero and is monotonically increasing, a Broker will only accept the message if the sequence number of the message is exactly one greater than the last committed message from that PID/TopicPartition pair. When it is not the case, the producer resends the message.

The Idempotent producer ensures Exactly Once Semantics message delivery per partition. To do so in multiple partitions, Kafka guarantees atomic transactions, which powers the applications to produce multiple TopicPartitions atomically. All writes to these TopicPartitions will either succeed or fail as a single unit. The application must provide a unique id, TransactionalId, to the producer, which is stable across all sessions of the application.....
        
        <Code>
{
    producer.initTransactions();
    try{
     producer.beginTransaction();
        producer.send(record0);
        producer.send(record1);
        producer.sendOffsetsToTxn(…);
        producer.commitTransaction();
    } catch( ProducerFencedException e) {
        producer.close();
    } catch( KafkaException e ) {
        producer.abortTransaction();
    }
} 
</Code>
        
What about consumer?
https://dzone.com/articles/kafka-clients-at-most-once-at-least-once-exactly-o
        

### If a new consumer joins a consumer group, how would the partitions be assigned to the new consumer?

Let’s say we have 1 topic with 3 partitions; and 1 consumer group consisting of 2 consumers. Out of the 3 partitions, 2 would be assigned to one consumer and the remaining partition would be assigned to the other consumer. Now, consider these two cases

- Case 1: If a new consumer joins the consumer group, rebalancing happens and each consumer is now assigned to a single partition (since we have equal number of partitions and consumers).
- Case 2: If a consumer goes down, then there’d be only 1 consumer left in the consumer group and all the partitions would be assigned to this consumer through rebalancing.

### What is rebalancing in Kafka?

A. Rebalancing is the re-assignment of partition ownership among consumers within a given consumer group such that every consumer in a consumer group is assigned one or more partitions. Rebalancing happens when:

- A new consumer joins the consumer group
- An existing consumer goes down
- New partitions are added
- An existing consumer is considered dead by the Group coordinator

### What is a Group coordinator?

A. A Group coordinator is a kafka broker which receives heartbeats from all consumers of a consumer group. Every consumer group has a group coordinator.


### What is a Group Leader?

A. The first consumer that joins a consumer group is called the Group Leader of that consumer group

### Can we decrease the number of partitions in a topic?

A. Apache Kafka doesn’t support decreasing the partitions of a topic. Since, all the data sent to a topic is sent to all the partitions and removing one of them means data loss.

### What is a Partition Leader in Kafka?

In Kafka, there is a concept of leader for each partition.

At any point in time, a partition can have only one broker as the leader. And only that leader can serve the data for the partition. Followers will sync the data from the leader.

### Replication in Kafka and ISR

In Kafka, replication happens at the partition level i.e. copies of the partition are maintained at multiple broker instances.

When we say a topic has a replication factor of 3, this means we will be having three copies of each of its partitions. Kafka considers that a record is committed when all replicas in the In-Sync Replica set (ISR) have confirmed that they have taking the record into account.

While creating a Kafka topic, we can define replication-factor, the number of copies we want to have for the data. We define this using the  config setting.

ISR indicates replicas are In Sync with the partition leader, i.e. those followers that have the same data as the leader.
  
    
### Can a Kafka broker have multiple partitions of same topic?
The short answer is YES. The same partition is identical on all brokers. Different partitions contain different messages. However, Kafka is a moving system, so not everything is aligned all the time.

Yes, a broker can handle numerous partitions on multiple topics. There is an overhead to having more partitions, so choosing the "right" number requires knowledge of many factors.    
    
Multiple partitions on a topic and these multiple partitions being consumed by multiple consumers within a single consumer group. That way you can achieve maximum throughput in your application. If you only use a single consumer thread for multiple partitions it would be of no use. Basically More partitions could lead to Higher throughput if you manage your cluster resources cleverly.

Create multiple partitions for the Topic in terms of parallelism/performance in the context of consumers. If you have multiple consumers in a single consumer group and multiple partitions in the topic, then it is guaranteed that consumers will receive data from different partitions which will give you parallelism and performance boost while processing from kafka. 

### How to auto-scale consumers through Kubernetes operator and HPA

Leverage k8s’s Operator pattern and Custom Resource Definition (CRD) to manage the life cycle of a Kafka consumer group running a top a k8s cluster.

Combination of _**record-lag metric**_ and number of partitions per topic are used to auto-scale consumers.
    
The new CRD KconsumerGroup is a Primary Resource and its spec describes the individual consumer specification such as consumer name, image, the topic it should poll messages from, minReplicas indicates the minimum number of consumers to start with, averageRecordsLagLimit set the threshold for HPA to scale out. In term of status, we want to see active pods and a customised message.

### How to setup Kafka on K8s?
    
https://medium.com/hacking-talent/mastering-apache-kafka-on-kubernetes-strimzi-k8s-operator-2c1d21d7b89a

#### Optimizations

- Use Kafka Consumer to batch push into Redshift

### Decoupling consumption and processing

**Multi-threaded Kafka consumer**

A naive approach might be to process each message in a separate thread taken from a thread pool, while using automatic offset commits (default config). Unfortunately, this may cause some undesirable effects:
- Offset might be committed before a record is processed
- Message processing order can’t be guaranteed since messages from the same partition could be processed in parallel.

While the goal is to achieve record processing parallelization, you also want your multi-threaded solution to maintain the features that a common, single-threaded approach has: processing order guarantees per partition and at-least-once delivery semantics.

The solution described in this blog post uses runnable tasks executed by a thread pool for processing records. The rest of this blog post describes how it works.

Note: This implementation might not be optimal for all use cases. Its goal is to demonstrate key aspects that need to be considered when implementing a multi-threaded consumer model.
Decoupling consumption and processing

In a multi-threaded implementation, the main consumer thread delegates records processing to other threads.

Records are retrieved using the poll method, the same as with a single-threaded implementation. Then, the records are grouped by partition, which results in multiple collections where each holds records from only a single partition. In order to process those collections, runnable tasks are created for each and submitted to an instance of Java’s built-in thread pool implementation.

<img src="https://cdn.confluent.io/wp-content/uploads/decoupling-consumption-600x344.png" width="60%" height="60%" />

[Source](https://www.confluent.io/blog/kafka-consumer-multi-threaded-messaging/)

In Spring Boot,

The @KafkaListener will create multiple consumers for you.

You can configure all of them to use the same topic and belong to the same group. The Kafka coordinator will distribute partitions to your consumers.

