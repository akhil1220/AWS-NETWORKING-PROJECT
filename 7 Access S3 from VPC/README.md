## Overview
This project demonstrates how resources inside and amazon VPC securely access AWS managed services that exist outside the VPC boundary. By connecting an EC2 instance to amazon S3 using IAM credentials and the AWS CLI, it highlights the distinction between network isolation and identity based access in AWS architectures.

## Architecture 


## Implementation 

## Step 1: Provision a network controlled environment

I created a amazon VPC with single public subnet to establish a minimal, observable networking boundary.

The VPC was intentionally kept small to clearly isolate how traffic exits the VPC when accessing external AWS services.

# Step 2: Launch compute inside VPC 

An EC2 instance was launched into public subnet with public IPV4 address enabled.

This allowed the instance to reach AWS public service endpoints and enabled access via EC2 Instance connect without introducing SSH Key management overhead.

## Step 3: Attempt service access with out credentials

From inside the EC2 instance i used AWS CLI to attempt listing s3 buckets using the command "aws s3 ls" .

The request failed as expected due to missing credentials demonstrating that network connectivity alone does not grant access to AWS services.

## Step 4: Configure IAM Based authentication 

I generated IAM Access keys and configured them on EC2 instance using " aws configure " .

This step established authenticated access to aws services and reinforced the seperation between identity (IAM) and networking (VPC).

## Step 5:  Create an Amazon s3 buckets and upload objects

I created an amazon s3 bucket in the same aws region as the VPC and uploaded two objects from my local machine.

This bucket served as External AWS Managed service that the EC2 instance would attempt to access.







