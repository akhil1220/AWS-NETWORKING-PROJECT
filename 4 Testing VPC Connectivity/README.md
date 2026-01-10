## Testing VPC Connectivity ##

 ## Overview ##
 This project demonstrates how to design, validate, and troubleshoot VPC connectivity in AWS by enabling secure communication:
 
 a)Between public and private EC2 instances
 
 b)Between a public EC2 instance and the public internet

 This Project follows real world cloud engineering practices including security hardnening processes by adding Network ACL's Security groups etc. And troubleshooting methodologies.

 ## Architecture ##

 ![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/046fd130ff2de3332fb6fd76822408fd12a97f5e/4%20Testing%20VPC%20Connectivity/architecture/part%204.drawio.png)

## Implementation ##
## Step 1: Connecting to the Public EC2 instance 

Used EC2 Instance Connect to establish SSH access directly from the AWS Console.

The intial result: Failed

## Step 2: Diagnose and fix SSH Connectivity issue 

To identify the root cause of the failed connection i validated all the networking layers which are related to inbound connectivity.

a) Route Table: Confirmed the public subnet had a default route (0.0.0.0/0) to the Internet Gateway.

b) Network ACLs: Verified inbound and outbound traffic were allowed.

c) Security Groups: Discovered that inbound rules only allowed HTTP traffic.

As the security group allows only HTTP traffic the ssh connection was failed but we need ssh also to be allowed in order to establish the connection.

# Resolution #
Added the inbound SSH (Port 22) rule for public subnet's security group. 

Hence the connection was established successfully.


![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/269cb049e073b42a2a42951c2ef44756d5c32d62/4%20Testing%20VPC%20Connectivity/screenshots/establshed%20Connection%20.png)


## Step 3: Testing connectivity between public and private EC2 instances 

With access to the public server established, I tested internal VPC communication.

Retrieved the private IPv4 address of the private EC2 instance.

Initiated connectivity testing using:
ping <private ip>

Result: No ping responses received.

Interpretation:

The lack of responses indicated that ICMP traffic was being blocked, even though routing between subnets was correct.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/af3e28825bb0cd1c4738ca12d340a698438f96ea/4%20Testing%20VPC%20Connectivity/screenshots/No%20ping%20response.png)

## Step 4: Identify Network ACL Restrictions on the Private Subnet 

I have evaluated Subnet level rules for private instance. Heres what i have identified 

a) Route table is correctly routed traffic within the VPC

b) In network ACL identified that all inbound and outbound traffic was denied.

This prevented the ICMP packets from reaching the private instance.

## Step 5: Allow ICMP Traffic at the Network ACL Level

So to allow the traffic i have updated the Private subnets network ACL to allow

a) Inbound ICMP (IPv4) from the public subnet CIDR

b) Outbound ICMP (IPv4) back to the public subnet

This modification allowed the ICMP Packets to pass at subnet level.

## Step 6: Allow ICMP Traffic at security group level

Security groups acts as instance level firewalls so  ICMP traffic should be permitted at security groups too.

To make this changes i have updated the security group to allow 

Inbound ICMP (IPv4) from the public instance’s security group

After making these changes i re ran the ping now i received ICMP replies.

 ## *Outcome* :
Confirmed successful and secure communication between public and private EC2 instances across subnets.

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/1b2ca6d0b499fbd73cd43891efcf20ecc531a18d/4%20Testing%20VPC%20Connectivity/screenshots/Replies.png)


## Step 7:Validate Internet Connectivity from the Public Subnet

To Confirm outbound internet access 

Executed HTTP Request from the public EC2 instance using  *curl example.com* 

![image alt]()






































