## Overview 

This project demonstrates how to monitor and analyze AWS Network traffic using AWS Flow Logs and Amazon Cloudwatch. I built multi VPC Architecture, Generated real traffic with EC2 instances and used flowlogs to troubleshoot connectivity issues and gain visibility into accepted and rejected network traffic.

## Architecture 

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/38699f6ca98cf0c0156c620d90a506e63b584d13/6%20VPC%20Monitoring%20with%20Flowlogs/Architecture/6%20architecture.drawio.png)

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


## Step 6: Analyzing network traffic with cloudwatch Logs insights

First i reviewed the flow logs recorded about vpc 1's public subnet.

The below are the log events recorded.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/bd62962d1222056c6fdf8c62a47dbd86128bd5eb/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/log%20events%20.png)

so when i expanded the last log i got this 

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/0db81ff70983333f3e24d834c85be897ce655f7b/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/expansion%20.png)

To break it down 
This flow log shows that 40 bytes of data were sent successfully from the IP address 185.114.175.11 to 10.1.13.142 on port 918 with 1 data packet transferred and the traffic was not allowed. (REJECT OK)

Next i analyzed the captured data with cloudwatch Logs insights, for that

i ran the query " Top 10 byte transfers by source and destination IP addresses "

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/0db81ff70983333f3e24d834c85be897ce655f7b/6%20VPC%20Monitoring%20with%20Flowlogs/screenshots/log%20insights.png)

Insights gained were 

1. Identified the most active traffic flows.
2. Observed accepted vs rejected traffic.
3. Mapped IP addressess back to EC2 instances and EC2 instance connect.

So this cofirmed that monitoring was working correctly and traffic patterns are aligned with expected network behaviour.

## Key learnings

1. Gained hands on experience on how to use VPC Flowlogs and Amazon Cloudwatch to monitor, capture and analyze network traffic.
2. Developed the ability to debug connectivity issues by distinguishing between routing problems and security group or NACL Misconfiguration.
3. Applied IAM least privilege principles by  by creating custom policies and service specific roles for secure logging.





































