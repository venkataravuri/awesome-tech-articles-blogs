
# AWS Topics

## Databases

## Amazon RDS

AWS Relational Database System. Allows to easily deploy single-machine or distributed instances of the most common databases (Oracle, SQL Server, MySQL, MariaDB, PostgreSQL) and Amazon’s own distributed relational database “Aurora”.

### Replication

Read replica replication is asynchronous
Replicas across AZs are synchronous
Read replicas are good for heavy queries (e.g. analytical queries for back office operations)
Read replica is supported for MySQL, MariaDB, and PostgreSQL as well as Amazon Aurora

### Encryption

Encryption at rest is supported for MySQL, SQL Server, Oracle and PostgreSQL & MariaDB.
Managed by AWS KMS.
Cannot encrypt an already present instance. To migrate an unencrypted DB to an encrypted one: create a new DB Instance with encryption enabled and then manually migrate your data into it.

:star::star: [See section Limitations of Amazon RDS Encrypted DB Instances](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html)

### Multi-AZ Deployment

A standby copy is created in another AZ. AWS handles replication and auto-failover
AWS can automatically failover RDS instance to another instance.
In case of failover, No need to change connection string.
This can be used for DR purpose only. This option has to be selected at instance creation time. This option is not useful for improving performance / scaling.

### Automatic failover of Multi AZ deployments

Events that would cause Amazon RDS to initiate a failover to the standby replica:

An Availability Zone outage
The primary DB instance fails
The DB instance’s server type is changed
The operating system of the DB instance is undergoing software patching
A manual failover of the DB instance was initiated using Reboot with failover
Limits
Maximum retention period for automated backup: 35 days
Other
Amazon RDS enables automated backups settings depends on the DB engine selected
RDS Provisioned IOPS (SSD) Storage is preferable for high-performance OLTP workloads
default metrics for RDS: The number of current connections to the database

### Read Replica Databases

Read-replica – async data transfer to another RDS instance. You can actually read from these instances, unlike Multi-AZ deployments. You can also have read replicas of read-replicas up to 5 copies. (Watch out as async causes latency)-

Read-replicas can be used for Dev/Test environments, run certain workloads only against them and not against direct production deployment – Intensive workloads.

MySQL , MariaDB, PostgreSQL only for read-replicas , no Oracle & SQL Server

You cannot have read-replicas that have multi-AZ. However, you can create read replicas of Multi AZ source databases.

Read replicas can be of a different size than source DB.

Each read-replica will have its own DNS end point

Automatic backups must be turned on in order to deploy a read replica

Read Replicas can be promoted to be their own databases. This breaks replication. E.g. Dev/Test can be connected to the replica by first promoting it as DB itself.

Read Replicas can be done in a second region for MySQL and MariaDB – no PostgreSQL.

Application re-architecture is required to make use of Read replicas

Read replicas are not used for DR. they are used for performance scaling only.

### Backups

Automated Backups – full daily snapshot & will also store transaction logs.

Enabled by default. Stored in S3. Free backup storage in S3 upto the RDS Instance size.

You can define backup window. Choose wisely.

Backups are deleted when the RDS Instance is deleted.

### Snapshots

Done manually. They are stored even after you delete the instance.

You can copy snapshots across regions.

You can publish the snapshot to make it publically available.

Restoring Backups/ Snapshots – The restored version will be a new RDS instance with new end point.

You can check the instance size to restore.

You cannot restore to existing instance


### DynamoDB

Fast and flexible NoSQL database

Consistent, single digit millisecond latency.

Fully managed DB – supports both document based & Key-value data models.

Great fit for mobile, IoT, web, gaming etc. applications.

Stored on SSDs

Stored on 3 geographically distinct DCs (not AZs). Built in redundancy

Consistency

Eventual consistent reads - Consistency reached up to 1 second (default)

Strongly Consistent reads - Consistency reached after writes to all copies are completed. <1 second

Select type based on application needs

Pricing – Write Capacity Units and Read Capacity Units ($/hr.). Also Storage cost per month. You provision capacity in units/second. It can scale on the fly. Provisioned capacity.

Dynamo DB – Expensive for Writes. Cheap for Reads. Important point v/s RDS.

You can dynamically add columns – without the need to update other rows with the column data. As this is no RDBMS.

Reserved capacity is available for DynamoDB as well.

#### RDS v/s DynamoDB

Use DynamoDB for Push button scaling. With RDS – to scale horizontally a new instance has to be created.

DynamoDB is cheap for reads and expensive for writes.

Observe workload characteristics and decide

Use RDS if data requires joins and relationships.

In RDBMS database structure cannot be dynamically altered. With DynamoDB you can.


#### Aurora

Bespoke Database Engine.

It is MySQL compatible.

However you can’t download and install on your workstation.

Performance
5 times better performance than MySQL. At a fraction of cost as compared to Oracle.

Scaling
Outset 10 GB Storage, auto increment of storage up to 64 TB

No Push button scaling – unlike DynamoDB

Fault Tolerance
Maintains 2 copies of your data in at least 3 availability zones. This is for the Data only not for the instances that runs the Database.

2 copies lost – no impact on write availability.

3 copies lost – no impact on read availability.

Storage is self-healing.

Pricing
Write and read throughput (1 capacity unit = 1 write/read per second).
Write capacity – billed in blocks of 10
Read capacity – charged in block of 50
You can change read/write capacity on the fly.
Storage costs per GB.

DynamoDB allows for the storage of large text and binary objects, but there is a limit of 400 KB.
With DynamoDB you provision an amount of transactions per second, and you can either manually increase/decrease this amount or configure auto scaling.

Replicas
MySQL Read Replica can be created from the Aurora source DB.(up to 5 of them)

Aurora Replicas – up to 15 of them. If leader crashes, the replica with the highest tiers becomes the leader. While creating replicas, remember to assign different tier levels.

Cluster Endpoint vs Individual Endpoint

No Free Tier usage available. Also available only in select regions. Takes slightly longer to provision

:star:star: https://aws.amazon.com/blogs/database/building-highly-available-mysql-applications-using-amazon-aurora-mmsr/



## Storage

## AWS S3

https://aws.amazon.com/about-aws/whats-new/2018/11/s3-intelligent-tiering/

S3 Intelligent-Tiering monitors access patterns and moves objects that have not been accessed for 30 consecutive days to the infrequent access tier.

 Service control policies (SCPs) are one type of policy that you can use to manage your organization. SCPs offer central control over the maximum available permissions for all accounts in your organization, allowing you to ensure your accounts stay within your organization's access control guidelines. See https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scp.html.

 * Retrieve object in parts—Using the Range HTTP header in a GET request, you can retrieve a specific range ofbytes in an object stored in Amazon S3.
 * Amazon S3 does not currently support Object Locking. If two PUT requests are simultaneously made to the same key, the request with the latest timestamp wins.

:star::star: SSE-KMS = envelope encryption - data key encrypted using the customer master key (CMK), can use stronger keys, extra cost, provides audit trail

:star::star:
Default Bucket Limit of 100 per account.


### AWS Elastic Block Storage (EBS)

EBS (Elastic Block Storage) provides block level storage. Offers storage volumes that can be attached as filesystems, like traditional network drives. You can install OS, Database on it, unlike S3.

EBS is a virtual disk. EBS Volumes can be mounted to an EC2 instance. They belong to 1 availability zone and are replicated across multiple physical disks.

EBS volumes can only be attached to one EC2 instance at a time. In contrast, EFS can be shared but has a much higher price point.

A standard block size for an EBS volume is 16kb.
EBS has an SLA with 99.95% uptime.
You CANNOT mount 1 EBS volume to multiple EC2 Instances. Use EFS instead.
EBS durability is reasonably good for a regular hardware drive (annual failure rate of between 0.1% - 0.2%). On the other hand, that is very poor if you don’t have backups! By contrast, S3 durability is extremely high. If you care about your data, back it up to S3 with snapshots.
RAID: Use RAID drives for increased performance.

EBS volumes for an instance are in the same AZ. You can only mount the EBS volumes in the same AZ as the EC2 instance.

EBS volume types and sizes can be changed on the fly, without any downtime. There is a performance hit for a bit.

Root device types can be EBS backed or instance backed.
Instance Store backed instances cannot be stopped and started, can only be rebooted.
Instance stores are ephemeral.
An instance can have many EBS volumes attached, but an EBS volume can be attached to only 1 instance at any time. There is no such thing as shared EBS, for that requirement, consider EFS.

#### EBS Volume Types

##### SSD Drives

(root volume) General Purpose SSD – up to 10,000 IOPS. 3 IOPS per GB. Balances price and performance. You can burst upto 3000 IOPS for 1GB
GP2 : General Purpose SSD, 3 IOPS per GB, bursts up to 10K IOPS, bursts up to 3000 IOPS for extended periods of time for volumes 3334 GB and above.


(root volume) Provisioned SSD – when you need more than 10,000 IOPS. Large RDBMS DBs and NoSQL DBs. Up to 20000 IOPS now.
Provisioned IOPS : More than 10K IOPS, can provision up to 20K IOPS per volume

One can provision IOPS (that is, pay for a specific level of I/O operations per second) to ensure a particular level of performance for a disk.

##### Magnetic Drives

HDD, Throughput Optimized– ST1 – Required for data written in sequence. Big Data, DWH, Log processing. Cannot be used as boot volumes
ST1 Throughput Optimized HDD : Cannot be boot volumes. DW, Logs are good use cases.

HDD, Cold– SC1 – Data that isn’t frequently accessed. E.g. File Server. Cannot be used as boot volume
SC1 Cold HDD : Cannot be boot volumes. Good for cold storage. Lowest cost.

(root volume) HDD, Magnetic (Standard) – Cheapest bootable EBS volume type. Used for apps where data is less frequently accessed and low cost is important.
Standard Magnetic : Legacy, can be bootable. cheapest bootable

The mim volume size for HDD is 500GB

##### EBS backups and snapshots

EBS snapshots sit on S3, and are incremental
Snapshots of an encrypted EBS volume will always be encrypted.
Snapshots can be shared with other accounts and can be made public. Encrypted snapshots cannot be shared.

You can back up the data on your Amazon EBS volumes to Amazon S3 by taking point-in-time snapshots. Snapshots are incremental backups, which means that only the blocks on the device that have changed after your most recent snapshot are saved. This minimizes the time required to create the snapshot and saves on storage costs by not duplicating data.

A snapshot is constrained to the region where it was created. After you create a snapshot of an EBS volume, you can use it to create new volumes in the same region. You can also copy snapshots across regions, making it possible to use multiple regions for geographical expansion, data center migration, and disaster recovery.
While snapshots are per region, volumes created from snapshots are tied to only a given availability zone in that region, so EBS Volumes cannot be attached to an EC2 instance in another AZ.

To take application consistent snapshots: Shut down the EC2 instance and detach the EBS volume, then take the snapshot.

The most resilient way to backup EBS disks is to take regular snapshots.

To move EBS volumes across AZs or Regions, use EBS snapshots.

Use Snapshot Copy to create a copy in a different region. Use Create Volume to create a new volume in a different AZ.

##### EBS encryption

EBS Root Volumes can be encrypted on custom AMIs only. Not on the default available AMIs. To encrypt root volumes, create a new AMI and encrypt root volume. You can also encrypt using 3rd party software like Bit Locker. Additional volumes attached to EC2 instance can be encrypted.

Snapshots of encrypted volumes are automatically encrypted.
Volumes that are created from encrypted snapshots are automatically encrypted.
When you copy an unencrypted snapshot that you own, you can encrypt it during the copy process.
When you copy an encrypted snapshot that you own, you can re-encrypt it with a different key during the copy process.

To encrypt an unencrypted EBS volume:
Create a snapshot
Copy the snapshot and select encryption
Create a volume from this encrypted snapshot
The only time an EBS volume can be create as an encrypted volume is during the creation.

### Storage Gateway

It is a service which connects an on-premises software appliance (virtual) with cloud based storage to provide seamless and secure connectivity between the two. Either via internet or Direct connect.
AWS Storage Gateway is a hybrid cloud storage service that gives you on-premises access to virtually unlimited cloud storage.

The AWS Storage Gateway service enables hybrid storage between on-premises environments and the AWS Cloud.

It provides low-latency performance by caching frequently accessed data on premises, while storing data securely and durably in Amazon cloud storage services.

Implemented using a virtual machine that you run on-premises (VMware or Hyper-V virtual appliance).

Provides local storage resources backed by AWS S3 and Glacier.

Often used in disaster recovery preparedness to sync data to AWS.

Useful in cloud migrations.

It is a service that allows an on-prem VM to S3 to migrate/replicate data
This VM can run with VMWare EXSi or Microsoft HyperV

They can all use DX or S2S VPN or Internet

The service provides three different types of gateways — Tape Gateway, File Gateway, and Volume Gateway

It can also provide connectivity from EC2 instance in VPC to S3 via Storage Gateway in same VPC

The virtual appliance will asynchronously replicate information up to S3 or Glacier

Can be downloaded as a VM – VMware ESXi / Hyper-V.

Storage Gateway is bridge between on-premises IT and cloud storage

Storage Gateway is a software appliance that sits on premises that can operate in three modes – gateway cached (hot data kept locally but most data stored in S3), gateway stored (all data kept locally but also replicated to S3) and VTL-Tape Library (virtual disk tapes stored in S3, virtual tape shelf stored in Glacier)

All data transferred between any type of gateway appliance and AWS storage is encrypted using SSL.

By default, all data stored by AWS Storage Gateway in S3 is encrypted server-side with Amazon S3-Managed Encryption Keys (SSE-S3).

#### 4 Types of Storage Gateways

AWS Storage Gateway supports three storage interfaces: file, volume, and tape.

You should use gateway cached when the requirement is for low cost primary storage with hot data stored locally

Gateway stored keeps all data locally but takes asynchronous snapshots to S3
Gateway cached volumes can store 32TB of data, 32 volumes are supported (32 x 32, 1PB)

Gateway stored volumes are 16TB in size, 12 volumes are supported (16 x 12, 192TB)

Virtual tape library supports 1500 virtual tapes in S3 (150 TB total)

Virtual tape shelf is unlimited tapes (uses Glacier)

Storage Gateway can be on premises or EC2. Can also schedule snapshots, supports Direct Connect and also bandwidth throttling.

Storage Gateway supports ESXi or Hyper-V, 7.5GB RAM, 75GB storage, 4 or 8 vCPU for installation. To use the Marketplace appliance, you must choose xlarge instance or bigger and m3, i2, c3, c4, r3, d2, or m4 instance types

The file gateway enables you to store and retrieve objects in Amazon S3 using file protocols, such as NFS. Objects written through file gateway can be directly accessed in S3.

##### Volumes Gateway

2.Volumes Gateway (iSCSI) – uses block based storage – virtual hard disk, operating system.

Stored Volumes – Store entire data set copy on-prem. Data async backed up to AWS S3.
Cached Volumes – Stored only recently accessed data on-prem. Rest on AWS S3
Volume gateway interface presents applications with disk volumes using iSCSI protocol. They take virtual hard disks on premise and back them up to virtual hard disks on AWS. Data written to these volumes can be asynchronously backed up as point in time snapshots of volumes and stored in cloud as EBS snapshots.

The volume gateway provides block storage to your applications using the iSCSI protocol. Data on the volumes is stored in Amazon S3. To access your iSCSI volumes in AWS, you can take EBS snapshots which can be used to create EBS volumes.

Gateway cached requires a separate volume as a buffer upload area and caching area

Gateway stored requires enough space to hold your full data set and also an upload buffer VTL also requires an upload buffer and cache area

Ports required for Storage Gateway include 443 (HTTPS) to AWS, port 80 for initial activation only, port 3260 for iSCSI internally and port 53 for DNS (internal)

Gateway stored snapshots are stored in S3 and can be used to recover data quickly. EBS snapshots can also be used to create a volume to attach to new EC2 instances

Can also use gateway snapshots to create a new volume on the gateway itself
Snapshots can also be used to migrate cached volumes into stored volumes, stored volumes into cached volumes and also snapshot a volume to create a new EBS volume to attach to an instance

Use System Resource Check from the appliance menu to ensure the appliance has enough virtual resources to run (RAM, vCPU, etc.)

Volume Gateway (block based, iSCSI, virtual hard disks where the AWS side is EBS)
Stored Volume - Entire copy is stored on-prem with async backups (incremental) to EBS as EBS snapshots. 1GB to 16TB storage limits.
Cached Volume - Only the most recently read data is kept on prem (vs. everything like Stored Volume Gateway). All the data is replicated on EBS. 1GB to 32TB storage limits.
VTL (Virtual Tape Library) or a Tape Gateway. Works with popular tape backup software to act as virtual tapes.

VOLUME GATEWAY
The volume gateway represents the family of gateways that support block-based volumes, previously referred to as gateway-cached and gateway-stored modes.

Block storage – iSCSI based.

Cached Volume mode – the entire dataset is stored on S3 and a cache of the most frequently accessed data is cached on-site.

Stored Volume mode – the entire dataset is stored on-site and is asynchronously backed up to S3 (EBS point-in-time snapshots). Snapshots are incremental and compressed.

Each volume gateway can support up to 32 volumes.

In cached mode, each volume can be up to 32 TB for a maximum of 1 PB of data per gateway (32 volumes, each 32 TB in size).

In stored mode, each volume can be up to 16 TB for a maximum of 512 TB of data per gateway (32 volumes, each 16 TB in size).


##### Gateway Virtual Tape Library (VTL)

3.Gateway Virtual Tape Library (VTL) – Backup and Archiving solution. Create tapes and send to S3. You can use existing backup applications like NetBackup, Backup Exec, and Veam etc.

VTL virtual tape retrieval is instantaneous, whereas Tape Shelf (Glacier) can take up to 24 hours

VTL supports Backup Exec 2012-15, Veeam 7 and 8, NetBackup 7, System Center Data Protection 2012, Dell NetVault 10

Snapshots can either be scheduled or done ad hoc

Writes to S3 get throttled as the write buffer gets close to capacity – you can monitor this with CloudWatch

The tape gateway provides your backup application with an iSCSI virtual tape library (VTL) interface, consisting of a virtual media changer, virtual tape drives, and virtual tapes. Virtual tape data is stored in Amazon S3 or can be archived to Amazon S3 Glacier

GATEWAY VIRTUAL TAPE LIBRARY
Used for backup with popular backup software.

Each gateway is preconfigured with a media changer and tape drives. Supported by NetBackup, Backup Exec, Veeam etc.

When creating virtual tapes, you select one of the following sizes: 100 GB, 200 GB, 400 GB, 800 GB, 1.5 TB, and 2.5 TB.

A tape gateway can have up to 1,500 virtual tapes with a maximum aggregate capacity of 1 PB.

##### File Gateway (NFS)

1.[Brand New] *File Gateway (NFS) – Just store files in S3 – Word, Pictures, PDFs, and no OS. ( Saves a lot of money) -Files are stored as objects in S3 buckets and accessed over NFS mount point -File attributes as stored as S3 object metadata. -Once transferred to S3, standard S3 features apply to all files.

File Gateway (uses NFS, only for file based) New Files are stored in S3 as objects. Think of this as an NFS interface to S3. Nothing is stored on-prem.

When using the file gateway, you can optionally configure each file share to have your objects encrypted with AWS KMS-Managed Keys using SSE-KMS.

FILE GATEWAY
File gateway provides a virtual on-premises file server, which enables you to store and retrieve files as objects in Amazon S3.

Can be used for on-premises applications, and for Amazon EC2-resident applications that need file storage in S3 for object based workloads.

Used for flat files only, stored directly on S3.

File gateway offers SMB or NFS-based access to data in Amazon S3 with local caching.

File gateway supports Amazon S3 Standard, S3 Standard – Infrequent Access (S3 Standard – IA) and S3 One Zone – IA.

File gateway supports clients connecting to the gateway using NFS v3 and v4.1.

Microsoft Windows clients that support NFS v3 can connect to file gateway.

The maximum size of an individual file is 5 TB.


## Amazon FSx

We recommend using AWS DataSync to transfer data between Amazon FSx for Windows File Server file systems. DataSync is a data transfer service that simplifies, automates, and accelerates moving and replicating data between on-premises storage systems and other AWS storage services over the internet or AWS Direct Connect

Amazon FSx for Lustre makes it easy and cost effective to launch and run the world’s most popular high-performance file system. Use it for workloads where speed matters, such as machine learning, high performance computing (HPC), video processing, and financial modeling.

### Snowball

The AWS Snowball service uses physical storage devices to transfer large amounts of data between Amazon Simple Storage Service (Amazon S3) and your onsite data storage location at faster-than-internet speeds.

https://docs.aws.amazon.com/snowball/latest/ug/images/Snowball-closed-600w.png

Snowball devices are physically rugged devices that are protected by the AWS Key Management Service (AWS KMS). They secure and protect your data in transit. Regional shipping carriers transport Snowballs between Amazon S3 and your onsite data storage location. 

Import-Export Disk’s successor
Puts data in S3 (and pulls from it if we want data exported out of AWS)
Called a suitcase at Marqeta :)
Petabyte Scale import/export appliance, up to 80TB.
Secure physically + encrypted (AES 256). Once the data is xfered, it goes through a complete wipe.
Snowball Edge is up to 100 TB and also has on-device compute capability. For example, the suitcase can run code to pull data in and store it.
Snowmobile is a truck, Exabyte scale data transfer. 100 PB storage limit.

f you need to transfer massive amount of data into AWS and it might take too long to do that on the wire you can use Snowball.
If your storage needs to exist also on premise (hybrid cloud storage), you can use Storage gateway.
