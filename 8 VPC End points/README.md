## Overview

This project demonstrates how to securely connect an amazon EC2 instance to an Amazon S3 bucket Using an AWS VPC endpoint ensuring traffic does not traverse the public internet.

S3 access is restricted using bucket and endpoint policies, allowing only private traffic from the VPC endpoint.

The implementation Highlights AWS Networking fundamentals, secure service access and best practices for cloud security.

## Architecture 

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/fd56a0fec30aef2a90af9859acb51786af8bb619/8%20VPC%20End%20points/Architecture/FINAL%20architecture.drawio.png)

## Implementation

## Step 1: Provision a network controlled environment

I created a amazon VPC with single public subnet to establish a minimal, observable networking boundary.

The VPC was intentionally kept small to clearly isolate how traffic exits the VPC when accessing external AWS services.

# Step 2: Launch compute inside VPC 

An EC2 instance was launched into public subnet with public IPV4 address enabled.

This allowed the instance to reach AWS public service endpoints and enabled access via EC2 Instance connect without introducing SSH Key management overhead.

# Step 3: Create an S3 bucket

Created a general purpose S3 bucket added two files from the local computer for validation and confirmed bucket availability in AWS Console.

# Step 4: Configure AWS CLI Access on EC2

-> Generated IAM Access key and secrete access key 

-> Configured AWS CLI using 

   " aws configure "

next verified access by listing S3 buckets

" aws s3 ls "

# Step 5: Access S3 via public internet

-> Listed objects in the bucket:

"aws s3 ls s3://thalari-bucket "

-> Uploaded a test file from EC2 to S3:

sudo touch /tmp/thalari.txt
aws s3 cp /tmp/thalari.txt s3://thalari-bucket


# Step 6: Create a VPC gateway endpoint for S3

Navigated to vpc endpoints and created endpoints by selecting gateway end point for amazon S3, attached endpoint to the VPC and associated endpoint with the public subnet route table.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/c1f0376a62362fae6bb3a742c523991ce0ee8bfe/8%20VPC%20End%20points/screenshots/VPC%20End%20points%20.png)

# Step 7: Secure the S3 Bucket with a Bucket Policy

Restricted the bucket access to only traffic from the VPC endpoints.

The below is the json code for the bucket policy i used.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/674820b52cbea8fecab0796d017c03653db1418a/8%20VPC%20End%20points/screenshots/bucket%20policy.png)

Result:

Console access to the bucket was denied and only end point traffic allowed.


# Step 8: Validated enpoint connectivity

Initial attempt failed due to missing route configuratio so i updated route table to forward S3 traffic to the endpoint.

# Step 9:  Test VPC Endpoint Policy Controls

Modified endpoint policy to Deny access → S3 access blocked.

Reverted policy to Allow → Access restored.


![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/448b690477cd3e3b004b4b4e7e96967a468769e7/8%20VPC%20End%20points/screenshots/Output.png)



## Key learnings:

VPC Gateway Endpoints enable private access to AWS services like Amazon S3, keeping traffic within the AWS network and eliminating exposure to the public internet.

S3 bucket policies and VPC endpoint policies provide layered security, allowing precise control over which networks and resources can access S3 data.

Correct route table configuration is critical for endpoint functionality, as traffic must be explicitly routed through the VPC endpoint for access to succeed.

























