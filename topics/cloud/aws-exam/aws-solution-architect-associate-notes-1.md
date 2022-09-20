# AWS Solution Architect Associate (SAA-C02) Notes

## Networking

### Fundamentals

[AWS Networking Fundamentals](https://youtu.be/hiKPPy584Mg)
https://www.youtube.com/watch?v=z07HTSzzp3o

## Compute

### EC2

Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud. AWS use Xen and Nitro Hypervisors.
- On Demand
- Reserved
- Spot
- Dedicated Hosts

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
