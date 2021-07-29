



~~~
Create the Transit Gateway
Navigate to Services.
Under Networking & Content Delivery, click VPC.
Click VPCs.
In the left sidebar menu, click Transit Gateways.
Click Create Transit Gateway.
Set the following values:
Name tag: MyTGW
Description: MyTGW
Amazon side ASN: 65065
Leave the rest as their defaults and click Create Transit Gateway.
Click Close.
Note: It may take a few minutes for the transit gateway to change from a pending state to an available state.

Transit Gateway Attachments
In the left sidebar menu, click Transit Gateway Attachments.
Click Create Transit Gateway Attachment.
Set the following values:
Transit Gateway ID: MyTGW
Attachment type: VPC
Attachment name tag: VPC1
DNS support: enable
VPC ID: VPC1
Under Subnet IDs, select us-east-1a as the Availability Zone and PublicSubnet1 as the Subnet ID.
Click Create attachment.
Click Close.
Click Create Transit Gateway Attachment, and set the following values for VPC2:
Transit Gateway ID: MyTGW
Attachment type: VPC
Attachment name tag: VPC2
DNS support: enable
VPC ID: VPC2
Under Subnet IDs, select us-east-1a as the Availability Zone and PublicSubnet2 as the Subnet ID.
Click Create attachment.
Click Close.
Click Create Transit Gateway Attachment, and set the following values for VPC3:
Transit Gateway ID: MyTGW
Attachment type: VPC
Attachment name tag: VPC3
DNS support: enable
VPC ID: VPC3
Under Subnet IDs, select us-east-1a as the Availability Zone and PublicSubnet3 as the Subnet ID.
Click Create attachment.
Click Close.
Routes
In the left sidebar menu, click Route Tables.
Select the Public1-RT route table.
Select the Routes tab and click Edit routes.
Click Add route and set the following values:
Destination: 10.2.0.0/16
Target: Transit Gateway
Click Save routes.
Click Close.
Select the Public2-RT route table.
Under the Routes tab, click Edit routes.
Click Add route and set the following values:
Destination: 10.1.0.0/16
Target: Transit Gateway
Click Save routes.
Click Close.
Testing
Open a terminal window.
Log in to INSTANCE1 via SSH using the provided lab credentials:

ssh cloud_user@<INSTANCE1_PUBLIC_IP_ADDRESS>
Ping the public IP address of INSTANCE2:

ping <INSTANCE2_PUBLIC_IP_ADDRESS>
Ping the private IP address of INSTANCE2:

ping <INSTANCE2_PRIVATE_IP_ADDRESS>
Ping the private IP address of INSTANCE3:

ping <INSTANCE3_PRIVATE_IP_ADDRESS>

~~~
