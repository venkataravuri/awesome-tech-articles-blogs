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

## PostgreSQL

#### Sharding in PostgreSQL

- PostgreSQL provides built-in sharding feature, uses a FDW-based approach (foreign data wrappers - FDW).
- The partitions are created on foreign servers and PostgreSQL FDW is used for accessing the foreign servers
- [PostgreSQL Sharding](https://wiki.postgresql.org/wiki/WIP_PostgreSQL_Sharding), [PostgreSQL Sharding Documentation](https://www.postgresql.org/docs/11/ddl-partitioning.html), [Sharding JDBC](https://shardingsphere.apache.org/document/legacy/4.x/document/en/manual/sharding-jdbc/)

**How to manage DB connection pool under sharded environment?**

In-appliction connection pool Vs. server-side connection pooling with `PGPool-II` or `PGBouncer`.

In-application pooling - create per-shard connection pools and pick a connection out of the appropriate pool for the shard. Since this will result in potentially large numbers of connections sitting around and lots of connects/disconnects, it will be very important to also run a server-side connection pool to limit and share connections to each shard. Use something like pgbouncer or pgpool-II in transaction pooling mode on each shard to share a relatively small number of real PostgreSQL connections out among the larger number of connections from web workers.


## AWS RDS - MySQL, PostgreSQL

### Zero-Downtime Maintenance

RDS requires some downtime during its patching and upgrades. To upgrade MySQL RDS to a new version, you have to perform an upgrade on RDS Read Replica first and then promote the replica to be a new master and finally switch your application to the new master. This procedure will result in a few minutes downtime.
 
RDS MySQL Aurora cluster which reduced the downtime to 30 seconds during the upgrades. Most recently Aurora provides zero-downtime patching, cutting downtime during upgrades to 5 seconds. 

RDS doesn’t officially support multi-master (M/M) replication. While RDS officially doesn’t support MySQL M/M, it doesn’t prevent you from implementing it on your own. 

Set up a M/M RDS before the maintenance and performed maintenance in the same fashion as our traditional approach on for MySQL hosted on EC2. The application writes to an active master only. However, during traffic switchovers both masters will be active for some short time. It allows us to perform zero-downtime upgrades via graceful switchovers and enjoy zero-downtime maintenances.

For those who got curious enough how does it work, here I will describe the steps on how do we configure M/M RDS. Otherwise, you can skip straight to the Conclusion.

- Launch new read replica (R1) (or use existing one if you can temporarily stop replication on it) to obtain the binlog position of the current existing Master (M1) from it. 
- Create a snapshot (SNAP1) from the R1 and launch a new RDS instance a future Master 2 (M2).

<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*vvH-Qb5qcAjHSALbMsbU6Q.png" width="50%" height="50%" />
