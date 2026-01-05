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

## SCREENSHOTS ##
https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/f60bd0a9c02d7d9c87d6068c6e26ad2075f16c04/01-Building%20VPCScreenshot/IGW.png
