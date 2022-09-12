# Kafka Internals, Scalability & Performance

<details>
<summary>How Kafka Nodes and zookeeper will communicate with each other?</summary>

Apache Kafka uses Zookeeper to select a controller, to maintain cluster membership and to store configuration, including the list of topics in the cluster.

In order to remain part of the Kafka cluster, each broker has to send keep-alive to Zookeeper in regular intervals. This is something every Zookeeper client does by default. If the broker doesn't heartbeat Zookeeper every zookeeper.session.timeout.ms milliseconds (6000 by default), Zookeeper will assume the broker is dead. This will cause leader election for all partitions that had a leader on that broker. If this broker happened to be the controller, you will also see a new controller elected.

https://stackoverflow.com/questions/54013250/how-kafka-nodes-and-zookeeper-will-communicate-with-each-other
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
    <summary>Is Zookeeper must for Kafka?<summary>
sssss
</details>

<details>
    <summary>Consumers partition allcoation</summary>
The consumers in a group divide the topic partitions as fairly amongst themselves as possible by establishing that each partition is only consumed by a single consumer from the group. When the number of consumers is lower than partitions, same consumers are going to read messages from more than one partition.

Ideally, the number of partitions should be equal to the number of consumers. Should the number of consumers be greater, the excess consumers were to be idle, wasting client resources. If the number of partitions is greater, some consumers will read from multiple partitions, which should not be an issue unless the ordering of messages is important.
</details>

## Kafka Engineering Blogs

https://blogboard.io/topic/Kafka

|Rating|Type|Topic
------------: | ------------- | -------------
|||[Kafka Redesign and Lessons Learned](https://www.moengage.com/blog/kafka-at-moengage/)|
|||[DoctorKafka: Kafka cluster healing and workload balancing](https://medium.com/pinterest-engineering/open-sourcing-doctorkafka-kafka-cluster-healing-and-workload-balancing-e51ad25b6b17)
|||[DoctorKafka: Kafka cluster healing and workload balancing](https://medium.com/pinterest-engineering/open-sourcing-doctorkafka-kafka-cluster-healing-and-workload-balancing-e51ad25b6b17)
|||[Running Kafka Streams applications in AWS](https://engineering.zalando.com/posts/2017/11/running-kafka-streams-applications-aws.html)



