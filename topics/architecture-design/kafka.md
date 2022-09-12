# Kafka Internals, Scalability & Performance

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
    /brokers: This contains alive brokers as well as topics configuration, assignments and current ISRs
    /controller: This ZNode is owned by the current controller in the Kafka cluster
    /admin: This contains delete topic requests
    /config: This contains overriden configs for brokers, quotas
    And the list goes on ...
https://stackoverflow.com/questions/54989802/where-kafka-store-the-meta-data-on-zookeeper-which-path
</details>


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

<details>
    <summary> What is a Group Leader?</summary>

A. The first consumer that joins a consumer group is called the Group Leader of that consumer group
</details>
    
<details>
    <summary>Can we decrease the number of partitions in a topic?</summary>

A. Apache Kafka doesn’t support decreasing the partitions of a topic. Since, all the data sent to a topic is sent to all the partitions and removing one of them means data loss.
</details>
    
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



