## PostgreSQL

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

# NoSQL & Databases

A curalted list of articles on database scalabilitiy, high availability and performance tuning.

MongoDB is strongly consistent by default - if you do a write and then do a read, assuming the write was successful you will always be able to read the result of the write you just read. This is because MongoDB is a single-master system and all reads go to the primary by default. If you optionally enable reading from the secondaries then MongoDB becomes eventually consistent where it's possible to read out-of-date results.
MongoDB also gets high-availability through automatic failover in replica sets: http://www.mongodb.org/display/DOCS/Replica+Sets

Mongostat
db.stats()

Phantom reads
A phantom read is a situation that occurs when two identical queries are executed and the collection of rows returned by the second query is different.

https://www.mongodb.com/developer/products/mongodb/everything-you-know-is-wrong/

## MongoDB

|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Active-Active Deployments - MongoDB](https://www.mongodb.com/blog/post/active-active-application-architectures-with-mongodb)

## MySQL, AWS RDS

|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Zero Downtime Maintenances on MySQL RDS](https://workmarket.tech/zero-downtime-maintenances-on-mysql-rds-ba13b51103c2)
||:newspaper:|[RazorPay: The Day of the RDS Multi-AZ Failover, Replication Failure & Data Loss](https://razorpay.com/blog/day-of-rds-multi-az-failover)

### Zero-Downtime Deployments

|Rating|Type|Topic
------------: | ------------- | -------------
||:newspaper:|[Demand Zero RPO and Zero Downtime for Business Success](https://www.cockroachlabs.com/blog/demand-zero-rpo/)
[Build highly available MySQL applications using Amazon Aurora Multi-Master](https://aws.amazon.com/blogs/database/building-highly-available-mysql-applications-using-amazon-aurora-mmsr/)


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


## Redshift

https://medium.com/doctolib/redshift-troubleshouting-made-simple-ed73b38d10d5
https://medium.com/develbyte/troubleshooting-in-redshift-c1ca4c7f7998


