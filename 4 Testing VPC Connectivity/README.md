## Testing VPC Connectivity ##

 ## Overview ##
 This project demonstrates how to design, validate, and troubleshoot VPC connectivity in AWS by enabling secure communication:
 
 a)Between public and private EC2 instances
 
 b)Between a public EC2 instance and the public internet

 This Project follows real world cloud engineering practices including security hardnening processes by adding Network ACL's Security groups etc. And troubleshooting methodologies.

## Implementation ##
## Step 1: Connecting to the Public EC2 instance 

Used EC2 Instance Connect to establish SSH access directly from the AWS Console.

The intial result: Failed

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/36530982fb8298fb9813d87f581d813e78456534/4%20Testing%20VPC%20Connectivity/screenshots/intial%20connection.png)

## Step 2: Diagnose and fix SSH Connectivity issue 

To identify the root cause of the failed connection i validated all the networking layers which are related to inbound connectivity.

a) Route Table: Confirmed the public subnet had a default route (0.0.0.0/0) to the Internet Gateway.

b) Network ACLs: Verified inbound and outbound traffic were allowed.

c) Security Groups: Discovered that inbound rules only allowed HTTP traffic.

As the security group allows only HTTP traffic the ssh connection was failed but we need ssh also to be allowed in order to establish the connection.

# Resolution #
Added the inbound SSH (Port 22) rule for public subnet's security group. 

Hence the connection was established successfully.

