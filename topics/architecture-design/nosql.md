# NoSQL DBs

- [MongoDB]()
- [AWS Redshift]()

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

### MongoDB Sharding

A **MongoDB sharded cluster** consists of the following components:
- **Shard**: Each shard contains a subset of the sharded data. Each **shard can be deployed as a replica se**t.
- **Mongos**: The mongos acts as a query router, providing an interface between client applications and the sharded cluster. Starting in MongoDB 4.4, mongos can support hedged reads to minimize latencies.
- **Config servers**: Config servers store metadata and configuration settings for the cluster.

MongoDB supports automatically ensuring data and requests are sent to the correct replica sets, and merging results from multiple shards.

<img src="https://www.mongodb.com/docs/manual/images/sharded-cluster-production-architecture.bakedsvg.svg" width="35%" height="35%" />

#### Shard Keys

MongoDB uses the shard key to distribute the collection's documents across shards. The shard key consists of a field or multiple fields in the documents.

To shard a collection, specify full namespace of the collection that you want to shard and the shard key. 

Use ```mongosh``` method ```sh.shardCollection()``` to shard a collection:
```
sh.shardCollection(<namespace>, <key>) // Optional parameters omitted
```

- namespace - Specify the full namespace of the collection that you want to shard ("<database>.<collection>").
- key - Specify a document { <shard key field1>: <1|"hashed">, ... } where
 * 1 indicates range-based sharding
 * "hashed" indicates hashed sharding.

#### MongoDB Tuning

Mongostat - db.stats()

### Additional Material

[Active-Active Deployments - MongoDB](https://www.mongodb.com/blog/post/active-active-application-architectures-with-mongodb)

## Time Series
|Rating|Type|Topic
------------: | ------------- | -------------
|:star::star:|:newspaper:|[Alibaba Cloud - Key Concepts and Features of Time Series Databases](https://www.alibabacloud.com/blog/key-concepts-and-features-of-time-series-databases_594734)
||:newspaper:|[Timescale - Time-series data: Why (and how) to use a relational database instead of NoSQL](https://www.alibabacloud.com/blog/key-concepts-and-features-of-time-series-databases_594734)

## Datawarehouse Concepts

Three Orthogonal concepts: 
- Data model - Star schema & Snowflake
- Workload characteristics (OLTP vs. OLAP)
- and Physical data organisation (columnar).

In a typical **_star schema_** world you will have **_dimension and fact_**. Mostly Dimensions are basically textual data and facts are numbers and generally dimension tables are small while fact table is large.

Snowflake schemas extend the star concept by further normalizing the dimensions into multiple tables. For example, a product dimension may have the brand in a separate table.

Star and snowflake schemas organize around a central fact table that contains measurements for a specific event, such as a sold item. The fact table has foreign key relationships to one or more dimension tables that contain descriptive attribute information for the sold item, such as customer or product. 

In columnar DBs you can avoid star schema. you don’t need to separate the textual and numerical values in separate table anymore as its taken care in columnar storage. So adding star schema on top of redshift will not make it efficient.

## AWS Redshift

* It is a OLAP database – Online analytics processing & Data warehouse service
* Massive parallel processing
* Columnar data storage, when storing data in columnar format Redshift uses a 1024Kb blocksize. Advanced compression due to columnar architecture.
* Doesn’t require indexes or materialized views.
* Amazon Redshift cluster consists of nodes
  * Each cluster has a _**leader node**_ and one or more _**compute nodes**_.
    * The leader node receives queries from client applications, parses the queries, and develops query execution plans.
    * The leader node then coordinates the parallel execution of these plans with the compute nodes and aggregates the intermediate results from these nodes.
* Amazon Redshift workload management (WLM) enables users to flexibly manage priorities within workloads so that short, fast-running queries won't get stuck in queues behind long-running queries.

[Redshift Architecture](https://docs.aws.amazon.com/redshift/latest/dg/c_high_level_system_architecture.html)

### Redshift Scalability & Performance Tuning

Redshift is a columnar database with compressed storage, it **doesn't use indexes like transactional databases** — such as MySQL, Microsoft SQL, and PostgreSQL — would. Instead, **it uses DISTKEYs and SORTKEYs**.

https://popsql.com/learn-sql/redshift/how-to-use-distkey-sortkey-and-define-column-compression-encoding-in-redshift

Redshift is an OLAP database, it’s oriented to work on analytical queries as opposed to OLTP with transactional queries

**It prefers to get a couple of big queries rather than a lot of small ones.**

You should avoid to,
- Stream events: prefer Kinesis or Lambda to aggregate bulk of data.
- Do multiple insert to load row by row. Prefer COPY.
- Connect a reporting tool directly on Redshift. Every common reporting tool has a cached/in-memory database. Put the Redshift data in it.

**Bad queues and WLM management**

Sometimes your queries are blocked by the “queues” aka “Workload Management” (WLM). Queues allow you to limit the number of parallel queries and the memory allocated to them, depending on the user or rules.

### Distkeys

The goal of distkeys is to avoid any broadcast of data between nodes. By doing so, you also want your nodes to be equally loaded. If data are not equally distributed, you will have “skewness”: the overloaded node will always be late compared to others.

When you create a table, you have 3 distribution styles called “distyle”: EVEN, ALL, JOIN

### Sortkeys

Redshift sorts the data into the blocks (1 MB) of slices (a part of a node) of nodes, and stores the possible values in a block zone map (min and max values). 

### System Tables 

`STV_RECENTS` — This table holds information about currently active and recently run queries against a database

```
-- displays every query that run or will run
SELECT user_name, db_name, pid, query
FROM stv_recents WHERE status = ‘Running’; -- displays every running queries
```

`STV_INFLIGHT` — Check the stv_inflight table, To find which queries are currently in progress.
```
SELECT * FROM stv_inflight;
```

`STV_LOCKS` — Amazon Redshift locks tables to prevent two users from updating the same table at the same time, STV_LOCKS can be used to view any current updates on tables in the database, need superuser to view

- **_svv_table_info_** - provides a lot of useful information on the performance health of your tables, including areas like,
 - table skew
 - Percent unsorted
 - Quality of the current table statistics
 - Sort key information

- Use the ANALYZE command to update the statistical metadata that the query planner uses to build and choose optimal plans.
- The VACUUM command is used to re-sort data added to non-empty tables, and to recover space freed when you delete or update a significant number of rows.

[Redshift Troubleshooting Guide - 1](https://medium.com/develbyte/troubleshooting-in-redshift-c1ca4c7f7998)
[Redshift Troubleshooting Guide - 2](https://medium.com/doctolib/redshift-troubleshouting-made-simple-ed73b38d10d5)
