# MySQL, PostgreSQL, AWS RDS

https://medium.com/@ronakdotpatel/rds-postgres-migration-with-zero-downtime-247eb4157260

### RPO & RTO
- [Demand Zero RPO and Zero Downtime for Business Success](https://www.cockroachlabs.com/blog/demand-zero-rpo/)

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
