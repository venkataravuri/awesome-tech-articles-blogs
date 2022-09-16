# Kafka Internals, Scalability & Performance

https://thanhnamit.netlify.app/2020/08/25/scaling-a-kafka-consumer-group-with-kubernetes-operator-and-hpa/

<details>
<summary>How Kafka Nodes and zookeeper will communicate with each other?</summary>

Apache Kafka uses Zookeeper to select a controller, to maintain cluster membership and to store configuration, including the list of topics in the cluster.

In order to remain part of the Kafka cluster, each broker has to send keep-alive to Zookeeper in regular intervals. This is something every Zookeeper client does by default. If the broker doesn't heartbeat Zookeeper every zookeeper.session.timeout.ms milliseconds (6000 by default), Zookeeper will assume the broker is dead. This will cause leader election for all partitions that had a leader on that broker. If this broker happened to be the controller, you will also see a new controller elected.

https://stackoverflow.com/questions/54013250/how-kafka-nodes-and-zookeeper-will-communicate-with-each-other
</details>

<details>
    <summary>Kafka No Longer Requires ZooKeeper (In future)</summary>

Until now, Apache ZooKeeper was used by Kafka as a metadata store. Metadata for partitions and brokers were stored to the ZooKeeper quorum that was also responsible for Kafka Controller election.

In upcoming release v2.8.0, ZooKeeper can be replaced by an internal Raft quorum of controllers. When Kafka Raft Metadata mode is enabled, Kafka will store its metadata and configurations into a topic called @metadata. This internal topic is managed by the internal quorum and replicated across the cluster. The nodes of the cluster can now serve as brokers, controllers or both (called combined nodes).
    https://towardsdatascience.com/kafka-no-longer-requires-zookeeper-ebfbf3862104 
</details>

<details>
    <summary>Where kafka store the metadata on zookeeper? ( which path? )</summary>

It depends which metadata!

By default, Kafka uses a number of paths in zookeeper:
- /brokers: This contains alive brokers as well as topics configuration, assignments and current ISRs (In-Syn Replicas)
    /controller: This ZNode is owned by the current controller in the Kafka cluster
    /admin: This contains delete topic requests
    /config: This contains overriden configs for brokers, quotas
    And the list goes on ...
https://stackoverflow.com/questions/54989802/where-kafka-store-the-meta-data-on-zookeeper-which-path
</details>

<details>
    <summary>Explan role of Kafka Controller?</summary>
Kafka controller is a thread that runs inside only one broker in a Kafka cluster i.e. If we have a cluster of N brokers then there will be only one broker that is the controller.

It is like a brain for the cluster so that the cluster functions in a smooth and resilient way.

Whenever a Kafka Cluster is spun up, the brokers will first create a session with the zookeeper and the brokers will try to create an ephemeral node “/controller” inside the zookeeper. The broker that will be able to successfully create the “/controller” node will become the controller.

The rest of the brokers will create a watch on this “/controller” node.
    
As soon as the controller goes down or its session with the zookeeper is lost then this znode will be deleted and the rest of the brokers will be notified, and a new controller will be elected again.
    
    In a Kafka cluster, one of the brokers serves as the controller, which is responsible for managing the states of partitions and replicas and for performing administrative tasks like reassigning partitions. At any given time there is only one controller broker in your cluster.
    
</details>

**_Transaction log is a Kafka Topic_**, it comes with the associated durability guarantees.

Producer Example: https://www.conduktor.io/kafka/complete-kafka-producer-with-java

Java Consumer Example: https://www.conduktor.io/kafka/complete-kafka-consumer-with-java

<details>
    <summary>Metadata requests in Kafka producer</summary>
The first time the producer makes a metadata request is when it connects to the bootstrap servers that you set in the client configuration. Of course, it can be just one broker or more but not necessarily all the brokers in the cluster (so the metadata request is not for each broker). In this way, the producer gets information about where are the topics that it wants to send messages. During its life, more metadata requests can be done when it receives an error connecting to the broker leader for the partition it's writing, in this case, it needs to know which broker is the new leader for connecting to it (if not connected yet for other topics) and starting to send.
https://stackoverflow.com/questions/56794122/metadata-requests-in-kafka-producer
</details>

<details>
    <summary>Consumers partition allcoation</summary>
The consumers in a group divide the topic partitions as fairly amongst themselves as possible by establishing that each partition is only consumed by a single consumer from the group. When the number of consumers is lower than partitions, same consumers are going to read messages from more than one partition.

Ideally, the number of partitions should be equal to the number of consumers. Should the number of consumers be greater, the excess consumers were to be idle, wasting client resources. If the number of partitions is greater, some consumers will read from multiple partitions, which should not be an issue unless the ordering of messages is important.
</details>
        
<details>
    <summary>Is having a Consumer Group mandatory in Kafka?</summary>

Yes, it is mandatory to specify Kafka which consumer would belong to which consumer group. If you do not set the consumer group id in your app, you will get an exception. If you start a consumer to consume from a topic using the Kafka CLI command, then a new random consumer group is created with the name console-consumer-<some_random_number> and the consumer automatically falls under this consumer group.
    
https://medium.com/javarevisited/kafka-partitions-and-consumer-groups-in-6-mins-9e0e336c6c00
    
</details>
    
    <details>
    <summary>Message Delivery Guarantees by Kafka?</summary>
Three different Message Delivery Guarantee types are supported by Kafka.

- Exactly once: Despite broker failures or producer retries, Kafka guarantees that every message will be stored only once, without duplications or data loss
- At-Least Once: Every message will always be saved in Kafka at least once, according to this rule. There is no chance of message loss, but if the producer tries again after the message has already been persisted, the message may be duplicated.
- At most Once: Every message in Kafka is only stored once, at most. If the producer doesn’t retry on failures, messages could be lost.

Source: https://hevodata.com/blog/kafka-exactly-once-semantics/#intro
        
Idempotent Producer?

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
        
</details>

<details>
    <summary>If a new consumer joins a consumer group, how would the partitions be assigned to the new consumer?</summary>

Let’s say we have 1 topic with 3 partitions; and 1 consumer group consisting of 2 consumers. Out of the 3 partitions, 2 would be assigned to one consumer and the remaining partition would be assigned to the other consumer. Now, consider these two cases

    Case 1: If a new consumer joins the consumer group, rebalancing happens and each consumer is now assigned to a single partition (since we have equal number of partitions and consumers).
    Case 2: If a consumer goes down, then there’d be only 1 consumer left in the consumer group and all the partitions would be assigned to this consumer through rebalancing.
</details>
    
<details>
    <summary>What is rebalancing in Kafka?</summary>

A. Rebalancing is the re-assignment of partition ownership among consumers within a given consumer group such that every consumer in a consumer group is assigned one or more partitions. Rebalancing happens when:

    A new consumer joins the consumer group
    An existing consumer goes down
    New partitions are added
    An existing consumer is considered dead by the Group coordinator
</details>
    
<details>
    <summary>What is a Group coordinator?</summary>

A. A Group coordinator is a kafka broker which receives heartbeats from all consumers of a consumer group. Every consumer group has a group coordinator.

</details>
    
<details>
    <summary> What is a Group Leader?</summary>

A. The first consumer that joins a consumer group is called the Group Leader of that consumer group
</details>
    
<details>
    <summary>Can we decrease the number of partitions in a topic?</summary>

A. Apache Kafka doesn’t support decreasing the partitions of a topic. Since, all the data sent to a topic is sent to all the partitions and removing one of them means data loss.
</details>
    
<details>
    <summary>What is a Partition Leader in Kafka?</summary>

In Kafka, there is a concept of leader for each partition.

At any point in time, a partition can have only one broker as the leader. And only that leader can serve the data for the partition. Followers will sync the data from the leader.
    </details>
    
<details>
    <summary>Replication in Kafka and ISR</summary>

In Kafka, replication happens at the partition level i.e. copies of the partition are maintained at multiple broker instances.

When we say a topic has a replication factor of 3, this means we will be having three copies of each of its partitions. Kafka considers that a record is committed when all replicas in the In-Sync Replica set (ISR) have confirmed that they have taking the record into account.

While creating a Kafka topic, we can define replication-factor, the number of copies we want to have for the data. We define this using the  config setting.

ISR indicates replicas are In Sync with the partition leader, i.e. those followers that have the same data as the leader.
    </details>
    
Can a Kafka broker have multiple partitions of same topic?
    The short answer is YES. The same partition is identical on all brokers. Different partitions contain different messages. However, Kafka is a moving system, so not everything is aligned all the time.

Can a broker have multiple partitions?
Yes, a broker can handle numerous partitions on multiple topics. There is an overhead to having more partitions, so choosing the "right" number requires knowledge of many factors.    
    
    
    multiple partitions on a topic and these multiple partitions being consumed by multiple consumers within a single consumer group. That way you can achieve maximum throughput in your application. If you only use a single consumer thread for multiple partitions it would be of no use. Basically More partitions could lead to Higher throughput if you manage your cluster resources cleverly.
    
    create multiple partitions for the Topic in terms of parallelism/performance in the context of consumers. If you have multiple consumers in a single consumer group and multiple partitions in the topic, then it is guaranteed that consumers will receive data from different partitions which will give you parallelism and performance boost while processing from kafka. 
    
Java Producer with Keys

Keys become useful when a user wants to introduce ordering and ensure the messages that share the same key end up in the same partition.



### How did you setup Kafka on K8s?
    
https://medium.com/hacking-talent/mastering-apache-kafka-on-kubernetes-strimzi-k8s-operator-2c1d21d7b89a
  

## Kafka Engineering Blogs

https://blogboard.io/topic/Kafka

|Rating|Type|Topic
------------: | ------------- | -------------
|||[Kafka Redesign and Lessons Learned](https://www.moengage.com/blog/kafka-at-moengage/)|
|||[DoctorKafka: Kafka cluster healing and workload balancing](https://medium.com/pinterest-engineering/open-sourcing-doctorkafka-kafka-cluster-healing-and-workload-balancing-e51ad25b6b17)
|||[DoctorKafka: Kafka cluster healing and workload balancing](https://medium.com/pinterest-engineering/open-sourcing-doctorkafka-kafka-cluster-healing-and-workload-balancing-e51ad25b6b17)
|||[Running Kafka Streams applications in AWS](https://engineering.zalando.com/posts/2017/11/running-kafka-streams-applications-aws.html)



