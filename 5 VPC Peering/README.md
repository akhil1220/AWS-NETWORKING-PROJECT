## VPC PEERING ##

## Overview ##
Setting up multiple VPC's and creating a peering connection and test VPC peering with connectivity tests.

Launched EC2 instances in each VPC and validated the connectivity while troubleshooting routing and security group issues.

## Architecture 

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/ccc22d9a87cb6e0757e59fb70727b3b39b6d563f/5%20VPC%20Peering/Architecture/Peering%20architecture.drawio.png)

## Implementation 

## 1. Created two  custom VPC's 

Created two seperate VPC's with non overlapping IPV4 CIDR blocks to ensure isolation.

Provisioned both VPC's using VPC and more wizard which automatically created essential resources 

Each VPC had only one public subnet.

## 2. Established VPC Peering connection

Created a VPC peering connection between the two VPC's designating one as the requester and other as acceptor. 

This enables traffic to flow directly between VPC's without using the public internet improving both security and performance.

## 3. Configured route tables for cross VPC traffic

After establishing Peering, route tables in both VPC's Were manually updated to direct traffic destined for peer VPC's CIDR block through peering connection.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/22c3876a64349d8681c0c2816e947a05d8d283a0/5%20VPC%20Peering/screenshots/VPC%20Peering%20.png)

Hence The peering connection is established successfully.


## 4. Launched EC2 instances in each VPC

Deployed one EC2 instance per VPC usng amazon linux 2023 AMI and t2.micro instance type.

when i tried to connect the first instance it showed an error stating "No public IPV4 address assigned"

Also the ssh was not allowed in the security group.

## Resolution 

In the first instance auto assign public ip was disabled so that is why the error showed up.

To fix this i allocated  Elastic IP to instance 1.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/f00a01a1e163bc55c0aada77b11fa4a5b3bfbe11/5%20VPC%20Peering/screenshots/elastic%20ip.png)

Then to fix the security group i have added a new rule to the First VPCs subnets security group which allows ssh.

Now the issue was resolved and the connection was successfull.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/8b060aaf1edd24681c394eb390b18a3ba27d12a4/5%20VPC%20Peering/screenshots/connection%201.png)


## 5. Tested VPC Peering using Ping (ICMP)

 To test the peering i used the IP address of the second instance and run command ping in first EC2 instance. the output was only one way.

 So to fix this i have gone through the security groups and found that ICMP traffic was not allowed in second VPC so added a new rule which allows ICMP traffic.

 The connection was successfull.

 ![image alt]( )



























