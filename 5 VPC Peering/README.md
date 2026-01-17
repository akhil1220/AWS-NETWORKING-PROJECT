## VPC PEERING ##

## Overview ##
Setting up multiple VPC's and creating a peering connection and test VPC peering with connectivity tests.

Launched EC2 instances in each VPC and validated the connectivity while troubleshooting routing and security group issues.

## Architecture 


## Implementation 

## 1. Created two  custom VPC's 

Created two seperate VPC's with non overlapping IPV4 CIDR blocks to ensure isolation.

Provisioned both VPC's using VPC and more wizard which automatically created essential resources 

Each VPC had only one public subnet.

## 2. Established VPC Peering connection

Created a VPC peering connection between the two VPC's designating one as the requester and other as acceptor. 

This enables traffic to flow directly between VPC's without using the public internet improving both security and performance.

## 3. Configured route tables for cross VPC traffic

After establishing Peering, route tables in both VPC's Were manually updated to direct traffic destined for peer VPC's CIDR block through peering connection.




