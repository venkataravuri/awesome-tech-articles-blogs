# MySQL, PostgreSQL, AWS RDS

- [DB Concepts]()
  - [Optimistic Lock Vs. Pessimistic Lock]()
  - [ACID Properties]()
    - [Read Phenomena]()
    - [Transaction Isolation Levels]()
    - [RPO & RTO]()
- [MySQL]()
- [PostgreSQL]()
- [AWS RDS]()

### DB Concepts

#### Optimistic Lock Vs. Pessimistic Lock

**Optimistic Locking** allows a conflict to occur, but it needs to detect it at write time. This can be done using either a physical or a logical clock. 

- Logical clocks are superior to physical clocks when it comes to implementing a concurrency control mechanism, 
- Use a **version column** to capture the read-time row snapshot information. The version column is going to be incremented every time an UPDATE or DELETE statement is executed while also being used for matching the expected row snapshot in the WHERE clause.

**Pessimistic locking** aims to avoid conflicts by using locking.

Pessimistic locking is suitable when the cost of retrying a transaction is very high or when contention is so large that many transactions would end up rolling back if optimistic locking were used.

- Pptimistic locking can help you **_prevent Lost Updates_** even when using application-level transactions that incorporate the user-think time as well.
- Optimistic locking works even across multiple database transactions since it doesn’t rely on locking physical records.

#### ACID Properties

A database transaction must satisfy the ACID property, which stands for Atomicity, Consistency, Isolation, and Durability.

**Read Phenomena**

A transaction can be interfered by other transactions that runs simultaneously with it. This interference will cause something we called _read phenomenon_.

- Dirty read –  A transaction reads data written by a concurrent uncommitted transaction.
- Nonrepeatable read –  A transaction re-reads data it has previously read and finds that data has been modified by another transaction (that committed since the initial read).
- Phantom read –  A phantom read is a situation that occurs when two identical queries are executed and the collection of rows returned by the second query is different.

**Transaction Isolation Levels**

- Read uncommitted - Transactions in this level can see data written by other uncommitted transactions
- Read committed - where transactions can only see data that has been committed by other transactions. Because of this, dirty read is no longer possible.
- Repeatable read -  ensures that the same select query will always return the same result, no matter how many times it is executed, even if some other concurrent transactions have committed new changes that satisfy the query.
- Serializable - Concurrent transactions running in this level are guaranteed to be able to yield the same result as if they’re executed sequentially in some order, one after another without overlapping.

https://medium.com/@ronakdotpatel/rds-postgres-migration-with-zero-downtime-247eb4157260

### RPO & RTO

**RPO** stands for Recovery Point Objective. RPO is the maximum amount of data loss it considers acceptable when a failure or outage occurs.

- RPO of ten minutes means, in the event of an outage, it can afford to lose up to ten minutes of data (lost transactions, etc.) before the company is seriously harmed.
- **Zero RPO** is how companies describe a setup in which no data loss is acceptable, even in the event of an outage.

Zero RPO systems can be more costly than less resilient, less available systems.

**RTO** stands for Recovery Time Objective. RTO is the maximum amount of application downtime it considers acceptable when a failure or outage occurs.

- RTO of ten minutes has decided that it can afford for its application to be offline for up to ten minutes in the event of an outage.
- Zero RTO is how companies describe a setup in which application downtime is never acceptable, even when an outage occurs.

### Zero-Downtime Maintenances
- [Zero Downtime Maintenances on MySQL RDS](https://workmarket.tech/zero-downtime-maintenances-on-mysql-rds-ba13b51103c2)
- [RazorPay: The Day of the RDS Multi-AZ Failover, Replication Failure & Data Loss](https://razorpay.com/blog/day-of-rds-multi-az-failover)
- [Build highly available MySQL applications using Amazon Aurora Multi-Master](https://aws.amazon.com/blogs/database/building-highly-available-mysql-applications-using-amazon-aurora-mmsr/)

#### Sharding PostgreSQL

- PostgreSQL provides built-in sharding feature, uses a FDW-based approach (foreign data wrappers - FDW).
- The partitions are created on foreign servers and PostgreSQL FDW is used for accessing the foreign servers
- [PostgreSQL Sharding](https://wiki.postgresql.org/wiki/WIP_PostgreSQL_Sharding), [PostgreSQL Sharding Documentation](https://www.postgresql.org/docs/11/ddl-partitioning.html), [Sharding JDBC](https://shardingsphere.apache.org/document/legacy/4.x/document/en/manual/sharding-jdbc/)

**How to manage DB connection pool under sharded environment?**

In-appliction connection pool Vs. server-side connection pooling with `PGPool-II` or `PGBouncer`.

In-application pooling - create per-shard connection pools and pick a connection out of the appropriate pool for the shard. Since this will result in potentially large numbers of connections sitting around and lots of connects/disconnects, it will be very important to also run a server-side connection pool to limit and share connections to each shard. Use something like pgbouncer or pgpool-II in transaction pooling mode on each shard to share a relatively small number of real PostgreSQL connections out among the larger number of connections from web workers.
