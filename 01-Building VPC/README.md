# Part 1 - Building  A Virtual Private CLoud 
## Creating a Custom VPC to understand how networking works in cloud ##
# ARCHITECTURE DIAGRAM #

## AWS Services used ## 
1. AWS VPC
2. Subnet
3. Internet gateway

## Implementation Steps  ##
1. First created a VPC with custom CIDR block IPV4 10.0.0.0/16 .
2. Created a subnet by selecting a availability zone and assigned CIDR as 10.0.0.0/24 . Also enabled auto assign IP.
3. Finally created a internet gate way and atached to the subnet.

## Screenshots ##
## *VPC* ##

![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/0d0ab26f3f67cbfb69a309be333cb525a4a72fbb/01-Building%20VPCScreenshot/VPC.png)

## *SUBNET* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/81e7c8fb7ab0285a462ddc77738e86c9cb0f1432/01-Building%20VPCScreenshot/SUBNET.png)


## *Internet Gateway* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/592d1c4cea9c8b80456e5af7ec1a12d0ee1d0a57/01-Building%20VPCScreenshot/IGW.png)
