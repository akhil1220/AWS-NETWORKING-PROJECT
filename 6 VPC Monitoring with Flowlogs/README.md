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

The problem identified was flow logs required explicit permissions to 

a) create log streams

b) write log events 

c) Describe log groups 











