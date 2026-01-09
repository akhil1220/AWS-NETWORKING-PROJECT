## Creating a pirvate subnet and launching VPC resources ##
## Overview ##
In this project i have created a private subnet and also launched resoures in both private and public subnet.

## Architecture ##
![image alt](https://github.com/akhil1220/AWS-NETWORKING-PROJECT/blob/429c108e3f715e916b784f35130bb1a75cc339c8/3%20-%20Private%20subnet%20and%20resource%20launching/Architecture/3%20And%204%20architecture.drawio.png)



## Steps to create a private subnet ##
1. I have used all the resources that i have created in my last project where i have created a **Virtual private cloud** and added required **public subnet, internet gateway, Network ACL and security group**.
2. Next  i created a private subnet and selected a different **Availability zone**. And also Assigned different **CIDR Block (10.0.1.0/24)**.
3 Added route table and attached to my private subnet.
4. Finally to round off i have set up a **Network ACL** and did not add any inbound and out bound rules for now. Then attached This Network ACL to private subnet.
5.  There is no need to create security groups until there is a specific resource.
6.  I did not add internet gateway because i dont need traffic from the internet as it is a Private subnet.

## Launching VPC Resources ##
1. Now to launch *PUBLIC* EC2 instance i selected launch instance then selected AMI and instance type.
2. For Key pair i used keypair type as RSA and private key pair format as .pem .Hence keypair is created.
3. Now atnetwork settings tab selected my current VPC, Public subnet and used the Secuirty group i created before.
4. The instacne is launched.
5. For *PRIVATE* EC2 instance same process is repeated like AMI, instace type keypair.
6. For security group i dont have any security grup for private subnet so i created here for creating the scurity group the type remains SSH and i used source type as custom and for source i selected my public security group source.
7. Click launch instance hence the instance is launched.

## Key learnings ##
1. AMI stands for amazon machine image. it is a prebuilt computers. it is a template used to create EC2 instances and contains the operating system along with the applications needed to launch the instance.
2. Key pair is used to help engineers to get direct access to the virtual machines. and RSA ia a type of cryptographic algorithm used.

## Screenshots ##
