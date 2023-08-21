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

## AWS RDS - PostgreSQL

[RDS Notes](https://github.com/venkataravuri/awesome-tech-articles-blogs/blob/master/topics/architecture-design/rdbms.md#aws-rds---mysql-postgresql)

### AWS Redshift

[AWS Redshift Notes](https://github.com/venkataravuri/awesome-tech-articles-blogs/blob/master/topics/architecture-design/nosql.md#aws-redshift)

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

#### How do you SSH to Bastion servers?
SSH Bastions as the entry point. The network path originates from the On-Prem network, goes through DX/VPN to the transit gateway (TGW), and then is routed to the Shared Services VPC.
