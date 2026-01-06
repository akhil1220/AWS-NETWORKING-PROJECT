## Creating a pirvate subnet and launching VPC resources ##
## Architecture ##




## steps to create A private subnet ##
1. I have used all the resources that i have created in my last project where i have created a **Virtual private cloud** and added required **public subnet, internet gateway, Network ACL and security group**.
2. Next  i created a private subnet and selected a different **Availability zone**. And also Assigned different **CIDR Block (10.0.1.0/24)**.
3 Added route table and attached to my private subnet.
4. Finally to round off i have set up a **Network ACL** and did not add any inbound and out bound rules for now. Then attached This Network ACL to private subnet.
5.  There is no need to create security groups until there is a specific resource.

## Launching VPC Resources ##
1.
