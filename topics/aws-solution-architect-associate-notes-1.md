# AWS Solution Architect Associate (SAA-C02) Notes

## Networking

### Fundamentals

[AWS Networking Fundamentals](https://youtu.be/hiKPPy584Mg)
https://www.youtube.com/watch?v=z07HTSzzp3o

## Compute

### EC2

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. AWS use Xen and Nitro Hypervisors.
On Demand
Reserved
Spot
Dedicated Hosts
Standard Reserved Instances cannot be moved between regions. You can choose if a Reserved Instance applies to either a specific Availability Zone, or an Entire Region, but you cannot change the region.

#### EC2 Virtualization History

[Brendan Gregg's Blog - AWS EC2 Virtualization 2017: Introducing Nitro](http://www.brendangregg.com/blog/2017-11-29/aws-ec2-virtualization-2017.html)

#### EC2 Instance

When you launch an instance, the root device volume contains the image used to boot the instance.

You can choose between,

AMIs were backed by Amazon EC2 instance store, which means the root device for an instance launched from the AMI is an instance store volume created from a template stored in Amazon S3.

![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/instance_store_backed_instance.png?raw=true)

AMIs were backed by Amazon EBS, which means the root device for an instance launched from  Amazon EBS snapshot referenced by the AMI you use.

![](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/images/ebs_backed_instance.png?raw=true)

AWS recommends use AMIs backed by Amazon EBS, because they launch faster and use persistent storage.

An Amazon EBS-backed instance can be stopped and later restarted without affecting data stored in the attached volumes.

[EBS-Backed Vs. Instance Store](https://web.archive.org/web/20140601070714/https://skeddly.desk.com/customer/portal/articles/1346918-ebs-backed-versus-instance-store)

https://github.com/agasthik/aws-csa-2017#ec2-instance-types

#### Instance Purchasing Options

Amazon AWS provides several options to purchase EC2 instances for optimizing costs, based on your expectations and requirements:
On-Demand Instances: You pay by the second, for EC2 instances launched
Scheduled Instances: You purchase EC2 instances, that are available always on the specified schedule, for a period of one-year
Reserved Instances (RI): You purchase EC2 instances that are available always at an important discount, for a period of one to three years.
Spot Instances (SI): You request not-used EC2 instances, lowering significantly your AWS EC2 instance costs
Dedicated Instances: You pay by the hour, to runningyourEC2 instances on single-tenant hardware
Dedicated Hosts: You pay for a dedicated physical host that to running your EC2 instances. You can bring your existing software licenses for reducing costs
When you want to reserve a computing capacity, acquire Scheduled Instances or Reserved Instances (RIs) for a determined Availability Zone (AZ).
The most cost-effective choice is Spot Instances if your applications can be interrupted and you’re flexible to choose when your applications can be executed
You can reduce costs and address compliance requirements using Dedicated Hosts and your existing software licenses
You obtain a significant discount on AWS EC2 instance usage using Standard Reserved Instances offer when you commit to an instance family during a time
If you need change your instance configuration during the term, Convertible Reserved Instances offer you that option and you still receive an interesting discount on your instance usage

#### EC2 Auto Scaling

Amazon EC2 Auto Scaling helps in automatically scaling the Amazon EC2 instances up and down as per the policies you define.

Before you can create Auto scaling group you need to create a launch configuration

Launch Configuration – Select AMI, Instance Type , Bootstrap script

No actual instances are created just with launch configuration

Auto scaling group – Set minimum size, spread it over subnets (AZs)- select all available AZs

Run health checks from ELB

Configure Auto scaling policy – Based on Alarm take action – trigger a new instance creation when CPU Utilization is greater than 90% for 5 minutes. You can also delete instance based on alarms

When Auto scaling group is launched it creates the instances based on definition.

Target Tracking Scaling Policies for Amazon EC2 Auto Scaling
PDF
Kindle
RSS

Step scaling is part of dynamic scaling. Target tracking scaling or step scaling (both are dynqmic scaling policies) can only define to maintain a target metric like CPU utilisation. But they can  define say add 10 instances, when the CPU util is between 60 and 70, for ex.


:star::star::star:
With ~*target tracking scaling*~ policies, you select a scaling metric and set a target value. 

Amazon EC2 Auto Scaling creates and manages the CloudWatch alarms that trigger the scaling policy and calculates the scaling adjustment based on the metric and the target value. 

The scaling policy adds or removes capacity as required to keep the metric at, or close to, the specified target value. In addition to keeping the metric close to the target value, a target tracking scaling policy also adjusts to changes in the metric due to a changing load pattern.

For example, you can use target tracking scaling to:

    Configure a target tracking scaling policy to keep the average aggregate CPU utilization of your Auto Scaling group at 40 percent.

    Configure a target tracking scaling policy to keep the request count per target of your Application Load Balancer target group at 1000 for your Auto Scaling group.



#### IAM Roles for EC2
Avoid using user credentials on servers

IAM roles can be assigned/replaced to existing EC2 instances using AWS CLI. Not through the console.

A trick is to assign policies to the existing role. This will avoid the need to create new instances.

Role assigned to instance is stuck to the lifetime of the instance – until you delete the role. Easier to modify existing role by adding / removing policies.

Roles are universal. Applicable to all regions.

#### Security Group

A Security Group is a virtual firewall for the EC2 instance, to control traffic to and from the instance. One EC2 can have many security groups associated with it.
By default, a security group would allow all outbound traffic to any destination, any protocol.
Any change made to a security group is applied immediately (like adding/removing ports, etc.)
Security Groups are stateful. When an inbound rule is added, outbound traffic is automatically allowed.
Security Group rules are only to allow traffic, not to deny. By default all inbound traffic is denied, all outbound traffic is allowed.
All VPCs get a default security group. This SG has only 1 rule, where all the instances associated with that SG can talk to each other (source is itself)

A security group acts as a virtual firewall for your instance to control inbound and outbound traffic. When you launch an instance in a VPC, you can assign up to five security groups to the instance.
Security groups act at the instance level.
First line of defense. Network ACLs are second line.

* The difference between Security Group and ACLs is that, Security Group act as a firewall for associated Amazon EC2 instances, controlling both inbound and outbound traffic at the instance level, while ACLs act as a firewall for associated subnets, controlling both inbound and outbound traffic at the subnet level.

* By default, security groups allow all outbound traffic. This means we only need to allow inbound traffic from application SG to database SG for it to be functional and meet security requirements.

1 instance can have multiple security groups. As each security group only "allows" inbound traffic, there will never be a conflict on security group rules.

Security groups are stateful.
Evaluate all rules before deciding whether to allow traffic


Security group changes are applied immediately.

Security groups are "stateful". Rules added as inbound rules – automatic outbound rules are added. Response back on the same channel. NACLs are stateless.

All inbound traffic is blocked by default. You have to allow specific inbound rules for protocols

All outbound traffic is allowed by default.

Only allow rules, no deny rules exist. Use NACLs to deny specific IPs

Any number of EC2 instances in a security group.

EC2 instances in the default security group can communicate with each other.

Multiple security groups can be attached to an instance.

#### Pricing Models

On Demand:
Pay fixed rate by the hour with no commitment
Users that want the low cost and flexibility of EC2
Apps with short term, spiky or unpredictable workloads that cannot be interrupted
Apps being developed or tested on EC2 for the first time
Reserved:
Provide capacity reservation and offer significant discount on the hourly charge for an instance (1-3 year terms)
Applications have steady state, or predictable usage
Apps that require reserved capacity
Users able to make upfront payments to reduce their total computing costs even further.
Spot:
Bid whatever price you want for instance capacity by the hour
When your bid price is greater than or equal to the spot price, your instance will boot
When the spot price is greater than your bid price, your instance will terminate with an hours notice.
Applications have flexible start and end times
Apps that are only feasible at very low compute prices
Users with urgent computing needs for large amounts of additional capacity
If the spot instance is terminated by Amazon EC2, you will not be changed for a partial hour of usage
If you terminate the instance yourself you WILL be charged for any partial hours of usage.

Dedicated Instances: You pay by the hour, to runningyourEC2 instances on single-tenant hardware

Dedicated Hosts: You pay for a dedicated physical host that to running your EC2 instances. You can bring your existing software licenses for reducing costs.

#### EC2 Placement groups
Logical grouping of instances within a single AZ

Instances can participate in low latency, 10 GBPs network.

#### CloudWatch
Default Metrics – Network, Disk , CPU and Status check ( Instance and System)

Memory – RAM is a custom metric

You can create custom dashboards all CloudWatch metrics.

CloudWatch alarms – set notifications when particular thresholds are hit.

CloudWatch events help you respond to state changes. E.g. run Lambda function in response to.

CloudWatch logs helps you monitor EC2 instance/application/system logs. Logs send data to CloudWatch

Standard monitoring 5 mins. Detailed monitoring 1 minute - out of free tier.

CloudWatch is for logging. CloudTrail is for auditing your calls.


|Sr. No| Family| Specialty| Use Case| Type|
| ------------- |:-------------:| -----:|-----:|-----:|
|1 |D2 |Dense Storage | File Servers / DWH / Hadoop | Storage Optimized|
|2| R4. R3| Memory Optimized|Memory Intensive / DBs|Memory Optimized|
|3|M4. M3|General Purpose|Application Servers|General Purpose|
|4|C4, C3|Compute Optimized|CPU Intensive Apps, DBs|Compute O|
|5|G2|Graphics Intensive|Video Encoding / 3D Application Streaming||
|6|I2|High speed storage (IOPS)|NoSQL DBs, DWH||
|7|F1|Field Programmable Gate Array|Hardware acceleration of Code||
|8|T2|Lowest Cost, General Purpose|Web Servers/ Small DBs| General Purpose|
|9|P2|Graphics / General Purpose GPU[Parallel Processing]|Machine Learning / Bit Coin Mining.| |
|10|X1|Memory Optimized|SAP HANA / Apache Spark| - |

Acronym – **DIRT MCG FPX*  -

*D – Density , I  - IOPS , R – RAM , T – cheap T2, M – Main Choice ( default) – Apps, C – Compute,  G – Graphics, F – FPGA , P – Graphics – Pics – Parallel Processing , X – Extreme Memory*  - *

Use M3 for general purpose instances – balanced compute, memory and network resources

[Exam Tip] You will be asked to provide which instance type to use for a given scenario. Usually 3 options are fictitious.

### Exam Tips

Why you can’t connect to DB Server from DMZ. Check the security group – if it is removed or added

Have separate groups for EC2 Instance and RDS Instance.

Multi-AZ for Disaster Recovery only. Not for performance improvement. For performance improvement use, multiple read-replicas

Dynamo DB v/s RDS

If you want push button scaling, without any downtown, you will always want to use DynamoDB.

With RDS scaling is not so easy, you have to use a bigger instance or add read replicas (manual process).

If you are using Amazon RDS Provisioned IOPS storage with a MySQL or Oracle database engine, what is the maximum size RDS volume you can have by default? – 6TB

What data transfer charge is incurred when replicating data from your primary RDS instance to your secondary RDS instance? - There is no charge associated with this action.

When you have deployed an RDS database into multiple availability zones, can you use the secondary database as an independent read node? – No

RDS automatically creates RDS Security Group w/ TCP port # 3306 enabled. 

In VPC Security Group, the answer would be YES because you will have manually specify access to port & protocol.

ElastiCache
ElastiCache is a web service that makes it easy to run in-memory cache in the cloud. Can serve a layer that helps enhancing performance compared to disk-based databases.
Good use case is when your database is a read-heavy and not prone to  to frequent change.
Supports two open-source in-memory caching engines
Redis – Multi-AZ capabilities, protocol compatible with memcached.
Memcached – No multi-AZ capabilities.

### AWS Simple Notification Service (SNS)

### AWS Global Accelerator

AWS Global Accelerator is a service that improves the availability and performance of your applications with local or global users. It provides static IP addresses that act as a fixed entry point to your application endpoints in a single or multiple AWS Regions, such as your Application Load Balancers, Network Load Balancers or Amazon EC2 instances.
https://www.youtube.com/watch?v=i3jjUghOXGs

### AWS CloudFront

block access for certain countries."

You can use geo restriction, also known as geo blocking, to prevent users in specific geographic locations from accessing content that you're distributing through a CloudFront web distribution.
https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/georestrictions.html

### Gateway VPC endpoints

![](https://docs.aws.amazon.com/vpc/latest/userguide/images/vpc-endpoint-s3-diagram.png)

VPC endpoints has two types: interface endpoints and gateway endpoints.

 VPC gateway endpoints which supported:Amazon S3 and DynamoDB

 VPC interface endpoints which supported a lot of aws service including RDS data API, but Interface endpoints are powered by AWS PrivateLink

### Route 53

Geolocation routing policy – Use when you want to route traffic based on the location of your users.

Geoproximity routing policy – Use when you want to route traffic based on the location of your resources and, optionally, shift traffic from resources in one location to resources in another.

## AWS Simple Workflow Service

Simple Workflow Service, allows to define and run background workflow composed by parallel or sequential steps. Also described as a fully-managed state tracker and task coordinator.

Simple WorkFlow service that makes it easy to coordinate tasks between machines and humans with a task oriented API.
This is amazon.com shopping experience for fulfillment.

Preferred to SQS with cases like order management where there might be manual steps (eg. packing and shipping a parcel) or message delivery needs to be more reliable (only once & in order).
When a workflow is not making progress is probably because of a missing manual interaction.

- Workflows can last for as long as 1 year
- SWF Starter is the actor that starts the workflow
SWF Decider is a program that controls the coordination of tasks.
- SWF Activity Worker is the code that executes to perform that task.
- SWF assigns a task to only one worker (no duplication at all)
- SWF Domain is the container that contains the related workflows, their tasks, etc.
- Build, run and scale background jobs or tasks that have sequential steps
- Way to process human oriented tasks using a framework
- SQS has a retention period of 14 days, vs SWF has up to a 1 year for work-flow executions
- "Task could take a month" = SWF, as SQS only has a 14 day retention
- Presents a task-oriented API, whereas SQS offers a message-oriented API
- Ensures a teaks is assigned only once and is never duplicated;
- SQS duplicate messages are allowed, and must be handled
- Keeps track of all tasks and events in an application, SQS would need an implementation of a custom application-level tracking mechanism
- A collection of work-flows is referred to as a domain
- Domains isolate a set of types, executions, and task lists from others within the same account
- You can register a domain by using the AWS console or using the RegisterDomain action in the SWF API
- Domain parameters are specified in JSON format
- SWF Actors:
  - Workflow starters - An application that can initiate a Workflow
  - Decider's - Control the flow or coordination of activity tasks such as concurrency, or scheduling in a work-flow execution; If something has finished in a work-flow (or fails), a decider decides what to do next
  - Activity Workers - Programs that interact with SWF to get tasks, process received tasks, and return the results
- Brokers the interactions between workers and the decider; Allows the decider to get consistent views into the progress of tasks and to initiate new tasks in an ongoing manner
- Stores tasks, assigns them to workers when they are ready and monitors their progress
- Ensures that a task is assigned only once and is never duplicated
- Maintains the application state durably, workers and decider's don't have to keep track of the execution state, and can run independently, with the ability to scale quickly
