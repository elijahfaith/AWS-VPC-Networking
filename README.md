# AWS-VPC-Networking
Building a basic virtual private cloud (VPC) in AWS 

Creating a VPC and subnettings 

A Virtual Private Cloud (VPC) in AWS is a logically isolated network dedicated to your AWS account, allowing you to run AWS resources like EC2 instances within a secure virtual network. VPCs provide control over network configurations, including IP address ranges, subnets, routing tables, and security settings.

![Screenshot (145)](https://github.com/user-attachments/assets/c2ca132d-d4e7-46de-8f38-49b122e41852)

![Screenshot (158)](https://github.com/user-attachments/assets/b20e814c-59d8-4f7d-87c0-b35df56be50c)

Subnets in AWS VPC
A subnet is a segment of a VPC’s IP address range, allowing you to place resources in isolated sections for better management. AWS provides two types of subnets:

Public Subnet: Accessible from the internet, designed for resources that need to be publicly available.
Private Subnet: Not directly accessible from the internet, usually for resources that require restricted access (like databases).
Subnetting a VPC
When you create a VPC, you specify an IP range (CIDR block), and subnets are created by subdividing this range. For example:

A VPC with a CIDR block of 10.0.0.0/16 can be divided into smaller subnets:
Public Subnet: 10.0.1.0/24 (provides 256 IPs)
Private Subnet: 10.0.2.0/24 (another 256 IPs)
Each subnet is associated with a route table that defines whether the subnet has access to the internet (via an internet gateway) or is restricted to internal traffic.

Route Tables with associated subnets
Route Table control the flow of network traffic within the VPC and to external networks.
- Public Route table to Public subnet
![Screenshot (156)](https://github.com/user-attachments/assets/d2ca75e2-27b9-4282-917a-dbf67693dc59)

- Private Route table to Private subnet
![Screenshot (157)](https://github.com/user-attachments/assets/d5fac2f5-3f4c-4df7-98ba-12a7abca9ec1)



Internet Gateway Setup

Internet Gateway (IGW): Allows public internet access for resources in public subnets

![Screenshot (159)](https://github.com/user-attachments/assets/d3b0f895-1eb4-4783-8653-00b86a37cca7)

Security Groups 

A Security Group in AWS acts as a virtual firewall for your resources within a VPC, controlling inbound and outbound traffic at the instance level. Security groups are essential for managing network access to and from EC2 instances AWS services within a VPC, it serves as a firewall with inbound and outbound rule.
Inbound and Outbound Rules: Security groups define specific rules for incoming (inbound) and outgoing (outbound) traffic. These rules specify the allowed protocols, port ranges, and IP addresses or CIDR ranges

Public Security Group allowing inbound SSH of port 22 from my Local machine IP addrress only 
![Screenshot (152)](https://github.com/user-attachments/assets/bc9a0d37-4569-4ba3-87c4-5e044ecd68e8)

Private Security Group
![Screenshot (160)](https://github.com/user-attachments/assets/3cd806af-3bef-47b7-81c6-a17e2716838d)
Allowing inbound SSH access from instances within the Public Subnet.

Launching an Instance from the Local Machine
From the Terminal (Git bash) 
ssh -i /path/to/your-key.pem ec2-user@your-instance-public-ip
This allows to access to the instance in AWS from your terminal
![Screenshot (153)](https://github.com/user-attachments/assets/b33cc5b5-dfa1-41a5-8766-73df482a3565)
To SSH from the the Public Instance to the Private instance, theres need to copy the Key Pair into the a directory in the Public Instance
scp -i "path/to/public-instance-key.pem" path/to/AWSStudentKey.pem ec2-user@public-instance-public-ip:~

![Screenshot (163)](https://github.com/user-attachments/assets/4439bb0d-78cc-4fa9-afa0-62953180925b)


To check for internet connectivity, then we must create a NAT Gatway which will allow us get control of private instance.
A NAT (Network Address Translation) Gateway is an AWS-managed service that allows instances in a private subnet to access the internet or other AWS services without exposing these instances to inbound internet traffic. The NAT Gateway serves as an intermediary between your private subnet and the public internet.
NAT Gateways provide a reliable, secure way for resources in private subnets to communicate with external resources, making them essential for network design in AWS.
![Screenshot (161)](https://github.com/user-attachments/assets/fed55ec6-f974-4042-920e-55a59184df34)
![Screenshot (162)](https://github.com/user-attachments/assets/cfa8c56b-4b9a-44f4-8d04-3f401bd715cd)

sudo ssh -i AWSStudentKey.pem private-ip you can then access internet connectivity
![Screenshot (164)](https://github.com/user-attachments/assets/e5259c91-3bf5-4c90-a8d2-1b6092dff390)

ping private ip of the private instance,
This will show the internet connectivity of the Private instance to Network.

![Screenshot (165)](https://github.com/user-attachments/assets/9b710861-4a34-4e28-a16b-e5dddc1136b4)











