# NoSQL DBs

A curalted list of articles on database scalabilitiy, high availability and performance tuning.

## MongoDB

MongoDB is a distributed document database. MongoDB allows to store hierarchical structured data in a document - which is (mostly) analogous to a JSON object. Documents are stored in a collection, which is really just a bucket of documents. Each document can have a different structure, or schema, from all the other documents in the collection. 

MongoDB is a BSON database. MongoDB isn't a JSON database. It supports extra data types, such as ObjectIds, native date objects, more numeric types, geographic primitives, and an efficient binary type, among others!

MongoDB is an ACID database. It supports atomicity, consistency, isolation, and durability.

- Updates to multiple parts of individual documents have always been atomi
- Since v4.0, MongoDB has supported transactions across multiple documents and collections. Since v4.2, this is even supported across shards in a sharded cluster.

Clusters are for redundancy, not scalability.

Clusters (we call them replica sets) need a minimum of 3 nodes in a cluster, to achieve quorum. Each server in the cluster holds a complete copy of all of the data in the database.

- MongoDB is strongly consistent by default - if you do a write and then do a read, assuming the write was successful you will always be able to read the result of the write you just read. This is because MongoDB is a single-master system and all reads go to the primary by default. If you optionally enable reading from the secondaries then MongoDB becomes eventually consistent where it's possible to read out-of-date results.
- MongoDB also gets high-availability through automatic failover in replica sets: http://www.mongodb.org/display/DOCS/Replica+Sets

### Scaling MongoDB

In the context of scaling MongoDB:

- **Replication** creates additional copies of the data and allows for automatic failover to another node. Replication may help with horizontal scaling of reads if you are OK to read data that potentially isn't the latest.
- **Sharding** allows for horizontal scaling of data writes by partitioning data across multiple servers using a shard key. It's important to choose a good shard key. For example, a poor choice of shard key could lead to "hot spots" of data only being written on a single shard.

Replication and sharding are typically combined to created a sharded cluster where each shard is supported by a replica set.

From a client application point of view you also have some control in relation to the replication/sharding interaction, in particular:
- Read preferences - to control the consistency of the data returned by the query. For example, a ReadConcern of majority tells MongoDB to only return data that has been replicated to a majority of nodes in the replica set.
- Write concerns - The write concern enables the application to specify the number of replica set members that must apply the write before MongoDB acknowledges the write to the application.

### MongoDB Sharded Cluster

A MongoDB sharded cluster consists of the following components:
- **Shard**: Each shard contains a subset of the sharded data. Each shard can be deployed as a replica set.
- **Mongos**: The mongos acts as a query router, providing an interface between client applications and the sharded cluster. Starting in MongoDB 4.4, mongos can support hedged reads to minimize latencies.
- **Config servers**: Config servers store metadata and configuration settings for the cluster.

MongoDB supports automatically ensuring data and requests are sent to the correct replica sets, and merging results from multiple shards.

<img src="https://www.mongodb.com/docs/manual/images/sharded-cluster-production-architecture.bakedsvg.svg" width="35%" height="35%" />

[How to shard a collection?](https://www.mongodb.com/docs/manual/core/sharding-shard-a-collection/)

#### How do you tune MongoDB?

Mongostat
db.stats()

### Additional Material

[Active-Active Deployments - MongoDB](https://www.mongodb.com/blog/post/active-active-application-architectures-with-mongodb)



### Database Sharding
|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Tinder - Geosharded Recommendations Part 1: Sharding Approach](https://medium.com/tinder-engineering/geosharded-recommendations-part-1-sharding-approach-d5d54e0ec77a)
||:newspaper:|[MongoDB Sharding](https://docs.mongodb.com/manual/sharding/)
||:newspaper:|[Sharding Pinterest: How we scaled our MySQL fleet](https://medium.com/pinterest-engineering/sharding-pinterest-how-we-scaled-our-mysql-fleet-3f341e96ca6f/)
||:newspaper:|[Sharding & IDs at Instagram](https://instagram-engineering.com/sharding-ids-at-instagram-1cf5a71e5a5c)
||:newspaper:|[Patpal - Application Design Considerations for Sharding High Volume Databases](https://medium.com/paypal-engineering/application-design-considerations-for-sharding-high-volume-databases-429b9455a6c3)
||:newspaper:|[Youtube - Scaling MySQL in the cloud with Vitess and Kubernetes](https://youtube-eng.googleblog.com/2015/04/scaling-mysql-in-cloud-with-vitess-and.html)

https://luanjunyi.medium.com/system-design-paradigm-sharding-77cb6498a6dc

https://docs.oracle.com/en/cloud/paas/nosql-cloud/csnsd/shard-keys-and-primary-keys.html)

## Time Series
|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[Alibaba Cloud - Key Concepts and Features of Time Series Databases](https://www.alibabacloud.com/blog/key-concepts-and-features-of-time-series-databases_594734)
||:newspaper:|[Timescale - Time-series data: Why (and how) to use a relational database instead of NoSQL](https://www.alibabacloud.com/blog/key-concepts-and-features-of-time-series-databases_594734)


## AWS Redshift

https://medium.com/doctolib/redshift-troubleshouting-made-simple-ed73b38d10d5
https://medium.com/develbyte/troubleshooting-in-redshift-c1ca4c7f7998

### Redshift Scalability

https://docs.aws.amazon.com/redshift/latest/dg/c_high_level_system_architecture.html

### Redshift Performance Tuning


## PostgreSQL

Phantom reads
A phantom read is a situation that occurs when two identical queries are executed and the collection of rows returned by the second query is different.

To guarantee true serializability PostgreSQL uses predicate locking, which means that it keeps locks which allow it to determine when a write would have had an impact on the result of a previous read from a concurrent transaction, had it run first.

Predicate locks in PostgreSQL, are based on data actually accessed by a transaction. These will show up in the pg_locks system view with a mode of SIReadLock.

The particular locks acquired during execution of a query will depend on the plan used by the query, and multiple finer-grained locks (e.g., tuple locks) may be combined into fewer coarser-grained locks (e.g., page locks) during the course of the transaction to prevent exhaustion of the memory used to track the locks.

The phenomena which are prohibited at various levels are:

- Dirty read –  A transaction reads data written by a concurrent uncommitted transaction.
- Nonrepeatable read –  A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).
- Phantom read –  A transaction re-executes a query returning a set of rows that satisfy a search condition and finds that the set of rows satisfying the condition has changed due to another recently-committed transaction.
- Serialization anomaly  – The result of successfully committing a group of transactions is inconsistent with all possible orderings of running those transactions one at a time.

- Read uncommitted
- Read committed
- Repeatable read
- Serializable
