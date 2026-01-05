##  VPC Traffic flow and security ##
## Overview ##
In this project i have created **Route tables** , **Security groups** and **Network ACL (Access control list)**.
## Architecture diagram ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/6e8b283b9957b4372058e0b1627c055bfca31964/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Architecture/Architecture%202.png)
## Steps followed ##
1. Created a **Route table** and attached to the **public subnet** by editing subnet association.
2. Next Created a **security group** and added inbound  rule.
3. Created **Network ACL** And created inbound and outbound rules.and then attached to subnet.


## Screenshots ##

## *NACL INBOUND* ##
![Image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/ea75dd2181a8bed9bc97c0b7309901d269751b25/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Screenshots/NACL%20IB.png)

## *NACL OUTBOUND* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/0599e6fe57d8b96e7c094879e9e65ede0967e79c/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Screenshots/NACL%20OB.png)

## *ROUTE TABLES* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/ea181b33c01b507a6044b3dc38042764f943ee03/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Screenshots/Route%20table.png)

## *SECURITY GROUP INBOUND* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/25773bf8b59ee8519d3c45d4bab9824c59d7c725/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Screenshots/Security%20ib.png)

## *SECURITY GROUP OUTBOUND* ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/0295d64770740084721da19210c8d56c25460218/02%20VPC%20TRAFFIC%20FLOW%20AND%20SECURITY/Screenshots/Security%20ob.png)

## Key learnings ##
- Learned about route tables and how they are used to distribute or send the data to its desitination
- Acheived an idea on security groups and learned how to update inbound rules.
- Learned about Rule number 100.
- Learned about Network ACL And rules.

## Next steps ##
In the next project i will extend this seup and build Private subnet.

