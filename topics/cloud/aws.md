# AWS

## Networking

- [AWS Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html)

- [AWS Direct Connect + AWS Transit Gateway + VPN](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-aws-transit-gateway-vpn.html)

## Identity & Access Managment

- [AWS IAM Users vs. IAM Roles](https://www.howtogeek.com/devops/iam-users-vs-iam-roles-which-one-should-you-use/) 

## RDS PostgreSQL

#### How failover works in RDS?

In an Amazon RDS Multi-AZ deployment, Amazon RDS automatically creates a primary database (DB) instance and synchronously replicates the data to an standby instance in a different AZ. When it detects a failure, Amazon RDS automatically fails over to a standby instance without manual intervention.

_Standby instance does not take traffic, you need to setup read replicas_. Latest AWS preview offering provides two read replicas in multi-AZ deployment.
 
https://aws.amazon.com/rds/features/multi-az/

#### How RDS instances are upgraded with near-zero downtime?

Hardware maintenance, OS patching, Databases Engine major version ugrade needs RDS upgrade regularly.

- For Multi-AZ deployments, Hardware & OS maintenance is applied to the secondary instance first, then the instance fails over, and then the primary instance is updated. Instance failover usually about 60 seconds)
- 
- Upgrades to the database engine level require downtime. In Multi-AZ deployment, both the primary and standby DB instances are upgraded at the same time using rolling upgrade. By using a read replica, you can perform most of the maintenance steps ahead of time and minimize the necessary changes during the actual outage.

During failover, Amazon does a DNS swap internally so that your RDS endpoint points to the right machine, so you may have to restart your web processes that point to the DB so that they reconnect to the DB and pull in the new IP from a new DNS lookup.

## Redshift

### Datawarehouse Concepts
Three Orthogonal concepts: 
- Data model - Star schema & Snowflake
- Workload characteristics (OLTP vs. OLAP)
- and Physical data organisation (columnar).

In a typical **_star schema_** world you will have **_dimension and fact_**. Mostly Dimensions are basically textual data and facts are numbers and generally dimension tables are small while fact table is large.

Snowflake schemas extend the star concept by further normalizing the dimensions into multiple tables. For example, a product dimension may have the brand in a separate table.

Star and snowflake schemas organize around a central fact table that contains measurements for a specific event, such as a sold item. The fact table has foreign key relationships to one or more dimension tables that contain descriptive attribute information for the sold item, such as customer or product. 

In columnar DBs you can avoid star schema. you don’t need to separate the textual and numerical values in separate table anymore as its taken care in columnar storage. So adding star schema on top of redshift will not make it efficient.

### Redshift Peformance Metrics

- **_svv_table_info_** - provides a lot of useful information on the performance health of your tables, including areas like,
 - table skew
 - Percent unsorted
 - Quality of the current table statistics
 - Sort key information

- Use the ANALYZE command to update the statistical metadata that the query planner uses to build and choose optimal plans.
- The VACUUM command is used to re-sort data added to non-empty tables, and to recover space freed when you delete or update a significant number of rows.
