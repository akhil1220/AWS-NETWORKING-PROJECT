## Overview
This project demonstrates how resources inside and amazon VPC securely access AWS managed services that exist outside the VPC boundary. By connecting an EC2 instance to amazon S3 using IAM credentials and the AWS CLI, it highlights the distinction between network isolation and identity based access in AWS architectures.

## Architecture 
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/6c5c2a9c490c19c5d68072975db8365e21f14a82/7%20Access%20S3%20from%20VPC/Architecture/Architecture%207.drawio.png)

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

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/a1666102c4ee93d807f46fb46124db78f23edb58/7%20Access%20S3%20from%20VPC/Screenshots/s3.png)

## Step 6: Access the S3 bucket from inside the VPC

From the EC2 instance i used AWS CLI to:

A) List all S3 buckets in the Account.

For this i used the command "aws s3 ls".

B) List objects inside the target s3 bucket.

For this i used the command aws s3 ls s3://Thalari-vpc-project

C) Upload a new file from EC2 instance to S3 bucket.

For this i used the command   "" sudo touch /tmp/test.txt ""  to create blank .txt file in EC2 instance 

Here 

sudo stands for "superuser do" and it's used when you're running a command that typicaly needs elevated user permissions, like installing software or creating new files.

touch is a standard command used to create an empty file if it doesn't exist. If it does exist, this command will update the file's timestamp (i.e. the last time it was accessed) instead.

/tmp/ is a common directory path (you can think of a directory path as layers and layers of folders) typically used for temporary files.

test.txt is the name of the empty file you're creating.

Next i ran the command aws s3 cp /tmp/test.txt s3://thalari-vpc-project

here aws s3 cp: is the command to copy files.

/tmp/test.txt is the source file path. It's saying that the file to copy is test.txt, which exists inside a folder called tmp.

s3://thalari-vpc-project is the destination path. It's saying that the file should be copied to the S3 bucket thalari-vpc-project.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/579e4276d7f52339b02faf2723504dbcdee6f283/7%20Access%20S3%20from%20VPC/Screenshots/ec2%20instance.png )

## New  S3 bucket list after the file uploaded 

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/579e4276d7f52339b02faf2723504dbcdee6f283/7%20Access%20S3%20from%20VPC/Screenshots/s3%20new%20.png)


## Key learnings:

1. VPC's provide network isolation not service isolation.
2. Access to AWS Services Is Governed by IAM, Not Network Reachability.
3. Authentication mechanisms Shape architecture and security 





