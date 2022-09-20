# AWS

## VPC

### Gateway VPC endpoints
VPC endpoints has two types:
- **Gateway endpoints** - VPC gateway endpoints which supported:Amazon S3 and DynamoDB
- **Interface endpoints** - VPC interface endpoints which supported a lot of aws service including RDS data API, but Interface endpoints are powered by AWS PrivateLink

## Networking

#### What is the difference between AWS Transit Gateway and VPC Peering?

https://devopsdice.com/difference-between-aws-transit-gateway-and-vpc-peering/

#### Security Group

A security group acts as a virtual firewall for EC2 instance to control inbound and outbound traffic.

- By default, a security group would allow all outbound traffic to any destination, any protocol. 
- Security Groups are stateful. When an inbound rule is added, outbound traffic is automatically allowed. 
- Security Group rules are only to allow traffic, no deny rules exist. Use NACLs to deny specific IPs.
- By default all inbound traffic is denied, all outbound traffic is allowed.
- Multiple security groups can be attached to an instance.

#### Difference between AWS Security Groups and NACL?
The difference between Security Group and NACLs is that, Security Group act as a firewall for associated Amazon EC2 instances, controlling both inbound and outbound traffic at the instance level, while ACLs act as a firewall for associated subnets, controlling both inbound and outbound traffic at the subnet level.
    
Securty Groups are first line of defense. Network ACLs are second line.

https://devopsdice.com/difference-between-aws-security-group-and-nacl/
https://visualstorageintelligence.com/chargeback-vs-showback/

- [AWS Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html)

- [AWS Direct Connect + AWS Transit Gateway + VPN](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-aws-transit-gateway-vpn.html)

## EC2

#### How EC2 Auto Scaling works?

Amazon EC2 Auto Scaling creates and manages the CloudWatch alarms that trigger the scaling policy and calculates the scaling adjustment based on the metric and the target value. 

For example, you can use target tracking scaling to:
- Configure a target tracking scaling policy to keep the average aggregate CPU utilization of your Auto Scaling group at 40 percent.
- Configure a target tracking scaling policy to keep the request count per target of your Application Load Balancer target group at 1000 for your Auto Scaling group.

Before you can create Auto scaling group you need to create a launch configuration

1. Launch Configuration – Select AMI, Instance Type , Bootstrap script. No actual instances are created just with launch configuration
2. Auto scaling group – Set minimum size, spread it over subnets (AZs)- select all available AZs
Run health checks from ELB
3. Configure Auto scaling policy – Based on Alarm take action – trigger a new instance creation when CPU Utilization is greater than 90% for 5 minutes. You can also delete instance based on alarms
4. When Auto scaling group is launched it creates the instances based on definition.


## Identity & Access Managment (IAM)

- [AWS IAM Users vs. IAM Roles](https://www.howtogeek.com/devops/iam-users-vs-iam-roles-which-one-should-you-use/) 

https://devopsdice.com/aws-iam-identity-and-access-management/

https://visualstorageintelligence.com/chargeback-vs-showback/

#### IAM Roles for EC2
- Avoid using user credentials on servers
- IAM roles can be assigned/replaced to EC2 instances.
- Roles are universal. Applicable to all regions.

## EKS

#### API Gateway integration with EKS
[API Gateway integration with EKS](https://aws.amazon.com/blogs/containers/integrate-amazon-api-gateway-with-amazon-eks/)

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



### Route 53

- Geolocation routing policy – Use when you want to route traffic based on the location of your users.
- Geoproximity routing policy – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.


#### CloudWatch

CloudWatch is for logging. CloudTrail is for auditing your calls.

Default Metrics – Network, Disk , CPU and Status check ( Instance and System). Memory – RAM is a custom metric

- CloudWatch alarms – set notifications when particular thresholds are hit.
- CloudWatch events help you respond to state changes. E.g. run Lambda function in response to.
- CloudWatch logs helps you monitor EC2 instance/application/system logs. Logs send data to CloudWatch
- Standard monitoring 5 mins. Detailed monitoring 1 minute - out of free tier.

