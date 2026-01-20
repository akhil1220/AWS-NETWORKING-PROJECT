## Overview 

This project demonstrates how to monitor and analyze AWS Network traffic using AWS Flow Logs and Amazon Cloudwatch. I built multi VPC Architecture, Generated real traffic with EC2 instances and used flowlogs to troubleshoot connectivity issues and gain visibility into accepted and rejected network traffic.

## Architecture 


## Implementation

## Step 1: VPC Architecture setup

I began designing multi VPC architecture with non overlapping CIDR blocks 10.1.0.0/16 and 10.2.0.0/16 using AWS VPC wizard. Each VPC contains one public subnet, internet gateway keeping design minimal while enabling external connectivity for testing purpose.

## Step 2: Launching EC2 Instance for traffic generation

One instance was launched in each VPC to generate real time traffic, These instnaces were placed in public subnets, assigned public IPV4 addressess and configured with security groups allowing ICMP traffic.

This setup enabled connectivity testing using both public and private IP addresses.

## Step 3: Implementing VPC Flow logs 

To enable network monitoring i first created log group  in AWS Cloud Watch with retention that never expires and standard log class.

Then in subnet level i created flow log keeping the filter to all and maximum aggregation interval as 1 minute. and i set destination as cloud watchlogs.

Under service role there is no IAM role designed for flow logs.


## Step 4: IAM Role and policy setup

So while configuring  a flowlog i have encountered a permission issue i.e., VPC flow logs could not write to cloud watch because there was no IAM Role existed. 

## *Problem* ##

identified was flow logs required explicit permissions to 

a) create log streams

b) write log events 

c) Describe log groups 

## *Solution* ##

1. I created A custom IAM Policy granting Cloudwatch logs permissions:

To create a policy i started with create policy and then chose json and deleted  everything in the policy editor.

Now i added the below json policy to the policy editor and created IAM Policy.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/46f047e212df4a65cfb50dcf2280caebf27725b4/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/IAM%20Policy.png)

2. Created an IAM Role with a custom trust policy allowing only "Service": " vpc-flow-logs.amazonaws.com "

the statement "Service": " vpc-flow-logs.amazonaws.com " means the trust policy specifically points to VPC flow logs as the only service that can use this role.

Hence the IAM role set up is done.

And now i finished creating the flow log By assigning the IAM role.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/dcc1a2eb7b986c9c10f00c0a6eb77bf721e29136/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/Flow%20log%20.png)


## Step 5: Debugging private IP connectivity failure (Testing vpc peering)

To test the connectivity of the first EC2 instance i tried connecting and the connection waas successfull. But when i used ping test to check the connectivity of second 
EC2 instance the ping to public IP address succeeded but the ping to private IP was failed.

## *Root cause analysis*

Security groups and network ACLS's were correctly configured which ruled out  filtering issues.

The real issue was missing routing between VPC's i.e., there was no direct path for private IP traffic 

## *Resolution* 

1. Created a VPC peering connection.
2. Updated both VPC route tables to route traffic to peer CIDR Blocks.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/6594f734cb67b1deaf8c6328d4b3d9588b5825af/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/peering.png)

Once it was done then the ping connectivity was successfull

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/6e1e0ae3553b66e4aa1f09e4150a00f6d7fe799d/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/successful%20connection.png)








































