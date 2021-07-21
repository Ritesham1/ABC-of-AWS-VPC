# ABC-of-AWS-VPC

# Creating a Basic VPC and Associated Components
Introduction
<br />In this hands-on text, we will learn to create a VPC with an internet gateway, as well as create subnets across multiple Availability Zones.

# Explore the Solution
Log in to the live AWS environment using your free-tier credentials. 
Make sure you're in the N. Virginia (us-east-1) region throughout the lab.

# Create a VPC
 Navigate to the VPC dashboard.
<br />Click Your VPCs in the left-hand menu.
<br />Click Create VPC, and set the following values:
<br />Name tag: myVPC
<br />IPv4 CIDR block: 172.16.0.0/16
<br />Leave the IPv6 CIDR block and Tenancy fields as their default values.
<br />Click Create.

# Create an Internet Gateway, and Connect It to the VPC
Click Internet Gateways in the left-hand menu.
Click Create internet gateway.<br />
Give it a Name tag of "IGW".<br />
Click Create internet gateway.<br />
Once it's created, click Actions > Attach to VPC.<br />
In the Available VPCs dropdown, select our myVPC.<br />
Click Attach internet gateway.<br />

# Create a Public and Private Subnet in Different Availability Zones
Create Public Subnet<br />
Click Subnets in the left-hand menu.<br />
Click Create subnet, and set the following values:<br />
Name tag: Public1<br />
VPC: myVPC<br />
Availability Zone: us-east-1a<br />
IPv4 CIDR block: 172.16.1.0/24<br />
Click Create.<br />

Create Private Subnet<br />
Click Create subnet, and set the following values:<br />
Name tag: Private1<br />
VPC: myVPC<br />
Availability Zone: us-east-1b<br />
IPv4 CIDR block: 172.16.2.0/24<br />
Click Create.<br />

# Create Two Route Tables, and Associate Them with the Correct Subnet
Create and Configure Public Route Table<br />
Click Route Tables in the left-hand menu.<br />
Click Create route table, and set the following values:<br />
Name tag: PublicRT<br />
VPC: myVPC<br />
Click Create.<br />
With PublicRT selected, click the Routes tab on the page.<br />
Click Edit routes.<br />
Click Add route, and set the following values:<br />
Destination: 0.0.0.0/0<br />
Target: Internet Gateway > IGW<br />
Click Save routes.<br />
Click the Subnet Associations tab.<br />
Click Edit subnet associations.<br />
Select our Public1 subnet.<br />
Click Save.<br />
<br /><br />
Create and Configure Private Route Table<br />
Click Create route table, and set the following values:<br />
Name tag: PrivateRT<br />
VPC: myVPC<br />
Click Create.<br />
With PrivateRT selected, click the Subnet Associations tab.<br />
Click Edit subnet associations.<br />
Select our Private1 subnet.<br />
Click Save.<br />

# Create Two Network Access Control Lists (NACLs), and Associate Each with the Proper Subnet
Create and Configure Public NACL<br />
Click Network ACLs in the left-hand menu.<br />
Click Create network ACL, and set the following values:<br />
Name tag: Public_NACL<br />
VPC: myVPC<br />
Click Create.<br />
With Public_NACL selected, click the Inbound Rules tab below.<br />
Click Edit inbound rules.<br />
Click Add Rule, and set the following values:<br />
Rule #: 100<br />
Type: HTTP (80)<br />
Port Range: 80<br />
Source: 0.0.0.0/0<br />
Allow / Deny: ALLOW<br />
Click Add Rule, and set the following values:<br />
Rule #: 105
Type: SSH (22)<br />
Port Range: 22<br />
Source: 0.0.0.0/0<br />
Allow / Deny: ALLOW<br />
Click Save.<br />
Click the Outbound Rules tab.<br />
Click Edit outbound rules.<br />
Click Add Rule, and set the following values:<br />
Rule #: 100<br />
Type: Custom TCP Rule<br />
Port Range: 1024-65535<br />
Destination: 0.0.0.0/0<br />
Allow / Deny: ALLOW<br />
Click Save.<br />
Click the Subnet associations tab.<br />
Click Edit subnet associations.<br />
Select the Public1 subnet, and click Edit.<br />

# Create and Configure Private NACL
Click Create network ACL, and set the following values:<br />
Name tag: Private_NACL<br />
VPC: myVPC<br />
Click Create.<br />
With Private_NACL selected, click the Inbound Rules tab below.<br />
Click Edit inbound rules.<br />
Click Add Rule, and set the following values:<br />
Rule #: 100<br />
Type: SSH (22)<br />
Port Range: 22<br />
Source: 172.16.1.0/24<br />
Allow / Deny: ALLOW<br />
Click Save.<br />
Click the Outbound Rules tab.<br />
Click Edit outbound rules.<br />
Click Add Rule, and set the following values:<br />
Rule #: 100<br />
Type: Custom TCP Rule<br />
Port Range: 1024-65535<br />
Destination: 0.0.0.0/0<br />
Allow / Deny: ALLOW<br />
Click Save.<br />
Click the Subnet associations tab.<br />
Click Edit subnet associations.<br />
Select the Private1 subnet, and click Edit.<br />
<br /><br />
# Conclusion : Congratulations 
