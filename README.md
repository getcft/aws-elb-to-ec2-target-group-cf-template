# aws-elb-to-ec2-target-group-cf-template

## Description:

This solution creates an [AWS VPC](https://aws.amazon.com/vpc/) environment that has 2 public zones and 2 private zones with an EC2 Target Group that has one EC2 linux instance in it and a [AWS ELB](https://aws.amazon.com/elasticloadbalancing/) (ALB) routing traffic to it.

The AWS CloudFormation template creates a AWS VPC with 2 public subnets and 2 private subnets with an EC2 Target Group that has one EC2 linux instance running Apache on port 80 in it and a public facing ELB (ALB) routing traffic on port 80 to the EC2 target group.

AWS Virtual Private Cloud (Amazon VPC) lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define.

AWS Elastic Load Balancing automatically distributes incoming application traffic across multiple targets, such as Amazon EC2 instances, containers, IP addresses, and Lambda functions. It can handle the varying load of your application traffic in a single Availability Zone or across multiple Availability Zones.

 AWS Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable compute capacity in the cloud

_***note AWS ELB and EC2 will incur costs**_

* [ELB pricing](https://aws.amazon.com/elasticloadbalancing/pricing/) resource used in example: 1 Application Load Balancer
* [EC2 pricing](https://aws.amazon.com/ec2/pricing/on-demand/) resource used in example: 1 t2.nano

## Prerequisites:

* AWS account and environment configured with AWS Credentials
* IAM user with AWSCloudFormationReadOnlyAccess, AmazonVPCFullAccess, AmazonEC2FullAccess
* This example works without modification in the following regions: us-west-1, us-west-2, us-east-1, us-east-2

## See how it works:

AWS Management Console

* Login to AWS Management Console
* Launch in CloudFormation elb-to-ec2-target-group-cf-template.yml (from the repo you cloned)

CloudFormation Fields

* Stack name (Enter a name to associate to your AWS VPC, ELB, EC2 deployment)
* SSHKeyName (Used for EC2 Instance)**Next**
* Continue choosing **Next**
* Click **Create**

## Test:

In the AWS Management Console you should be able to verify the following have been created:

* 1 Public Subnet 10.0.10.0/24 (Zone A)
* 1 Private Subnet 10.0.20.0/24 (Zone A)
* 1 Public Subnet 10.0.30.0/24 (Zone B)
* 1 Private Subnet 10.0.40.0/24 (Zone B)
* 5 Route table entries to route either within 10.0.0.0/16 or to the either the Internet Gateway or NAT Gateway for outbound
* 1 Internet Gateway
* 1 ELB Security Group with Port 80 open to everyone
* 1 EC2 Security Group with Port 22 open to everyone and Port 80 open to the Load Balancer
* 1 ELB - Application Load Balancer
* 1 EC2 t2.nano linux instance
* 1 EC2 Target Group

You can find in the CloudFormation Outputs section the "ALBHostName" copy the hostname from the "Value" column and paste it into a browser you should see the word "Healthy" return.

## Other Things:

* You would normally put your EC2 instance or instances in a private subnet but to save costs for this example we didn't provision a NAT Gateway but needed to install Apache so we elected to put it in a public subnet.
