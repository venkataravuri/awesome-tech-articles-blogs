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

Security Group is a stateful firewall for the EC2 instances to control inbound and outbound traffic. It acts like a virtual firewall that can be attached to the instance or instances.

- By default, a security group would allow all outbound traffic to any destination, any protocol. 
- Security Groups are stateful. When an inbound rule is added, outbound traffic is automatically allowed. 
- Security Group rules are only to allow traffic, no deny rules exist. Use NACLs to deny specific IPs.
- By default all inbound traffic is denied, all outbound traffic is allowed.
- Multiple security groups can be attached to an instance.

#### NACL

NACL is a stateless virtual firewall that works at the subnet level. Everything both Inbound and Outbound traffic is allowed in default NACL. In NACL you need to specify explicitly what to block in Inbound and Outbound Rules.

#### Difference between AWS Security Groups and NACL?
- Security Group act as a firewall for associated Amazon EC2 instances, controlling both inbound and outbound traffic at the instance level.
- NACLs act as a firewall for associated subnets, controlling both inbound and outbound traffic at the subnet level.
    
Securty Groups are first line of defense. Network ACLs are second line.

### Chargeback vs Showback

Chargebacks work by notifying departments of the costs of their technology usage and simultaneously requiring payment. Often, this payment occurs automatically as a budget deduction.

- Chargebacks require payment directly from departments themselves.
- With chargebacks, each department is responsible for its own IT budget.

**Showback**
- Showbacks work by preparing a document (similar to a billing statement) that shows the cost of technology usage (such as a storage array or a software license).
- This document is typically shared with the department using the technology, but the department is not expected to pay for it through their budget.

## AWS Direct Connect

AWS Direct Connect makes it easy to establish a dedicated connection from an on-premises network to one or more VPCs.

- It uses industry-standard 802.1Q VLANs to connect to Amazon VPC using private IP addresses.

<img src="https://docs.aws.amazon.com/images/whitepapers/latest/aws-vpc-connectivity-options/images/image6.png" width="60%" height="60%" />

[AWS Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html)

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

<img src="https://devopsdice.com/wp-content/uploads/2022/03/IAM-1.png" width="50%" height="50%" />

- User – End-user or one specific individual person. So these are the people logging into the console and also interacting with us by running API commands.
- Groups – A collection of users under one set of permissions. For example, your marketing team might need access to read and write certain files stored in the S3 bucket and they’re going to need a specific set of permissions to allow them to do this. So it makes sense to create a group with the required permissions and then all you need to do is add the relevant users into that group and they will all have permissions.
- Role – You create roles and can then assign them to AWS Services, or external services/users.
- Policies – A document that defines one or more permissions. Policies can be attached to a user, group, or role.

#### IAM Roles for EC2
- Avoid using user credentials on servers
- IAM roles can be assigned/replaced to EC2 instances.
- Roles are universal. Applicable to all regions.

#### IAM Policies

- **Anatomy of a policy**: JSON doc with Effect, Action, Resource, Conditions, Policy Variable
- Explicit DENY has precedence over ALLOW

Sample Policy JSON
```
{
  "Version": "2012–10–17",
  "Statement": [
    {
      "Sid": "FirstStatement",
      "Effect": "Allow",
      "Action": [
		"ec2:AttachVolume",
		"ec2:DettachVolume"
		]
      "Resource": "arn:aws:ec2:*:*:instance/*",
	  "Condition":{
		"StringsEqual": {"ec2:ResourceTag/Department": "Development"}
	  }
    },
	{
      "Sid": "SecondStatement",
      "Effect": "Allow",
      "Action": [
		"ec2:AttachVolume",
		"ec2:DettachVolume"
		]
      "Resource": "arn:aws:ec2:*:*:volume/*",
	  "Condition":{
		"StringsEqual": {"ec2:ResourceTag/VolumeUser": "${aws:username}"}
	  }
    }
  ]
}
```

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
