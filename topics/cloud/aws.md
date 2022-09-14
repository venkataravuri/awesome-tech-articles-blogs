# AWS Notes

- [AWS IAM Users vs. IAM Roles](https://www.howtogeek.com/devops/iam-users-vs-iam-roles-which-one-should-you-use/) 

- [AWS Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html)

- [AWS Direct Connect + AWS Transit Gateway + VPN](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect-aws-transit-gateway-vpn.html)


## AWS RDS

#### How failover works in RDS?

In an Amazon RDS Multi-AZ deployment, Amazon RDS automatically creates a primary database (DB) instance and synchronously replicates the data to an instance in a different AZ. When it detects a failure, Amazon RDS automatically fails over to a standby instance without manual intervention.
 
https://aws.amazon.com/rds/features/multi-az/

#### How RDS instances are upgraded with near-zero downtime?

Hardware maintenance, OS maintenance, Databases Engine maintenance needs RDD upgrade regularly.



