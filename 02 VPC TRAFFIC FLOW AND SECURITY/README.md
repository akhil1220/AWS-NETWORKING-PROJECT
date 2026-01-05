##  VPC Traffic flow and security ##
## Overview ##
In this project i have created **Route tables** , **Security groups** and **Network ACL (Access control list)**.
## Architecture diagram ##

<pre>
+----------------------------------+
|        VPC (10.0.0.0/16)         |
|                                  |
|   +--------------------------+   |
|   |     Internet Gateway     |   |
|   +------------+-------------+   |
|                |                 |
|   +--------------------------+   |
|   |      Route Table         |   |
|   |  0.0.0.0/0 → IGW         |   |
|   +------------+-------------+   |
|                |                 |
|   +--------------------------+   |
|   |      Public Subnet       |   |
|   |      (10.0.0.0/24)       |   |
|   |   +------------------+   |   |
|   |   |  Security Group  |   |   |
|   |   +------------------+   |   |
|   +--------------------------+   |
|          Network ACL             |
+----------------------------------+
</pre>

## Steps followed ##
1. Created a **Route table** and attached to the **public subnet** by editing subnet association.
2. Next Created a **security group** and added inbound  rule.
3. Created **Network ACL** And created inbound and outbound rules.and then attached to subnet.


## Screenshots ##


## Key learnings ##
- Learned about route tables and how they are used to distribute or send the data to its desitination
- Acheived an idea on security groups and learned how to update inbound rules.
- Learned about Rule number 100.
- Learned about Network ACL And rules.

## Next steps ##
In the next project i will extend this seup and build Private subnet.

