# VPC


# Create a VPC

```
Navigate to the VPC dashboard.
Click Your VPCs in the left-hand menu.
Click Create VPC, and set the following values:
Name tag: VPC1
IPv4 CIDR block: 172.16.0.0/16
Leave the IPv6 CIDR block and Tenancy fields as their default values.
Click Create.

```

# Create an Internet Gateway, and Connect It to the VPC

```

Click Internet Gateways in the left-hand menu.
Click Create internet gateway.
Give it a Name tag of "IGW".
Click Create internet gateway.
Once it's created, click Actions > Attach to VPC.
In the Available VPCs dropdown, select our VPC1.
Click Attach internet gateway.
Create a Public and Private Subnet in Different Availability Zones
Create Public Subnet
Click Subnets in the left-hand menu.
Click Create subnet, and set the following values:
Name tag: Public1
VPC: VPC1
Availability Zone: us-east-1a
IPv4 CIDR block: 172.16.1.0/24
Click Create.
Create Private Subnet
Click Create subnet, and set the following values:
Name tag: Private1
VPC: VPC1
Availability Zone: us-east-1b
IPv4 CIDR block: 172.16.2.0/24
Click Create.

```

# Create Two Route Tables, and Associate Them with the Correct Subnet

```

Create and Configure Public Route Table
Click Route Tables in the left-hand menu.
Click Create route table, and set the following values:
Name tag: PublicRT
VPC: VPC1
Click Create.
With PublicRT selected, click the Routes tab on the page.
Click Edit routes.
Click Add route, and set the following values:
Destination: 0.0.0.0/0
Target: Internet Gateway > IGW
Click Save routes.
Click the Subnet Associations tab.
Click Edit subnet associations.
Select our Public1 subnet.
Click Save.
Create and Configure Private Route Table
Click Create route table, and set the following values:
Name tag: PrivateRT
VPC: VPC1
Click Create.
With PrivateRT selected, click the Subnet Associations tab.
Click Edit subnet associations.
Select our Private1 subnet.
Click Save.

```


# Create Two Network Access Control Lists (NACLs), and Associate Each with the Proper Subnet

```

Create and Configure Public NACL
Click Network ACLs in the left-hand menu.
Click Create network ACL, and set the following values:
Name tag: Public_NACL
VPC: VPC1
Click Create.
With Public_NACL selected, click the Inbound Rules tab below.
Click Edit inbound rules.
Click Add Rule, and set the following values:
Rule #: 100
Type: HTTP (80)
Port Range: 80
Source: 0.0.0.0/0
Allow / Deny: ALLOW
Click Add Rule, and set the following values:
Rule #: 110
Type: SSH (22)
Port Range: 22
Source: 0.0.0.0/0
Allow / Deny: ALLOW
Click Save.
Click the Outbound Rules tab.
Click Edit outbound rules.
Click Add Rule, and set the following values:
Rule #: 100
Type: Custom TCP Rule
Port Range: 1024-65535
Destination: 0.0.0.0/0
Allow / Deny: ALLOW
Click Save.
Click the Subnet associations tab.
Click Edit subnet associations.
Select the Public1 subnet, and click Edit.
Create and Configure Private NACL
Click Create network ACL, and set the following values:
Name tag: Private_NACL
VPC: VPC1
Click Create.
With Private_NACL selected, click the Inbound Rules tab below.
Click Edit inbound rules.
Click Add Rule, and set the following values:
Rule #: 100
Type: SSH (22)
Port Range: 22
Source: 172.16.1.0/24
Allow / Deny: ALLOW
Click Save.
Click the Outbound Rules tab.
Click Edit outbound rules.
Click Add Rule, and set the following values:
Rule #: 100
Type: Custom TCP Rule
Port Range: 1024-65535
Destination: 0.0.0.0/0
Allow / Deny: ALLOW
Click Save.
Click the Subnet associations tab.
Click Edit subnet associations.
Select the Private1 subnet, and click Edit.

```


