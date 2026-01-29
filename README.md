# Overview

Designed and implemented an AWS networking architecture to understand how cloud networks are built,
secured, monitored, and debugged n real worls environments.

This project focuses on practical engineering skills like designing VPC architectures, controlling traffic flow, trobleshooting connectivity failures, monitoring network traffic, and securely accessing AWS managed services without exposing resources to the public internet.

# Architecture

# What this project demonstrates

1. Custom VPC creation with non overlapping IP addressing.
2. Public and private subnet design isolation across availability zones
3. Layered traffic control using security groups, route tables and Networks ACL's.
4. Connectivity testing and troubleshooting of SSH, ICMP, Routing and  IAM failures.
5. Multi VPC connectivity using VPC peering.
6. Network observability using VPC flow logs and CloudWatch Logs insights.
7. IAM based access to AWS services from within a VPC.
8. Private amazon S3 access using VPC Gateway endpoints and policies.

# Project phases:

## *Phase 1: Custom VPC Design* 
Built a non default VPC with isolated IP addressing and internet connectivity.

## *Phase 2: Traffic Flow and Security*
Implemented routing, security grouos and NACL's to control inbound and outbound traffic>

## *Phase 3: Public and Private Subnets*
Deployed EC2 instances with strict access boundaries and controlled communication paths.

## *Phase 4: Connectivity and Testing*
Validated and troubleshoot SSH, ICMP, and Internet connectivity.

## *Phase 5: VPC peering*
Connected multiple VPC's and solved routing and security issues.

## *Phase 6: Network Monitoring*
Enabled VPC Flow logs, integrated Cloudwatch, and analyzed the traffic.

## *Phase 7: IAM based S3 access*
Demonstrated that AWS service access is done by IAM not VPC networking.

## *Phase 8: Private S3 access via VPC endpoint*
Secured S3 access using gateway endpoints, bucket and endpoint policies.




# Troubleshooting Highlights:

## *SSH access to public EC2 failed*

Route cause: 
Security group allowed HTTP not SSH.

Fix:
Resolved by allowing port 22. i.e., added inbound SSH rule.

## *No ICMP response between public and private EC2 instances*

Route cause:
ICMP was beign blocked at security group level and NACL.

Fix:
Allowed ICMP traffic at both layers i.e., security Group and NACL.

## *VPC Flow logs not writing to CloudWatch*

Route cause: Missing IAM permissions.

Fix: Created custom IAM policy and service role.

## *S3 Access via VPC endpoint initially failed*

Route cause: Route table not associated with the endpoint

FIX: Updated route table to route S3 traffic through endpoint.



# Security practices applied:

1. Least previlaged IAM policies.
2. Layered security i.e., routing + subnet + instance.
3. Private subnet isolation and no internet exposure for the private workloads
4. Explicit routing and policy enforcement.

# Key Learnings:

1. Netwprking issues must be done by debugging layer by layer.
2. Routing, NACLs and security group must all align for traffic to flow.
3. Monitoring and logs plays cruicial role for identifying route cause.
4. IAM controls access to AWS dervices not VPC networking.
5. Private architectures reduce exposures ad improve security.
   
## Repository Structure

```text
AWS-NETWORKING-PROJECT/
├── 01-Building-VPC/
├── 02-VPC-Traffic-Flow-and-Security/
├── 03-Private-Subnet-and-Resources/
├── 04-Testing-VPC-Connectivity/
├── 05-VPC-Peering/
├── 06-VPC-Monitoring-with-FlowLogs/
├── 07-Access-S3-from-VPC/
└── 08-VPC-Endpoints/
```







   
