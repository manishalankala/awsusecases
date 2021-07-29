




![image](https://user-images.githubusercontent.com/33985509/127530481-d64145c0-a053-44cf-b906-cd3e8fcbab05.png)


![image](https://user-images.githubusercontent.com/33985509/127530626-1145a2c4-91b4-4c8b-ac09-6f04362701ad.png)


![image](https://user-images.githubusercontent.com/33985509/127530696-233a9ca0-5400-4f2b-90c2-227b56b9af76.png)


![image](https://user-images.githubusercontent.com/33985509/127530834-c78b60ae-cccd-45f4-8bff-d5815e245dd1.png)


![image](https://user-images.githubusercontent.com/33985509/127531054-1e5eb8f7-19d1-4d1d-8646-b8ee6e185c47.png)


![image](https://user-images.githubusercontent.com/33985509/127531376-fe6c1d58-2590-44d5-8526-cde5734d00fb.png)


![image](https://user-images.githubusercontent.com/33985509/127531494-7fd1cfbf-8a31-4249-9001-b325ad6d0afe.png)


![image](https://user-images.githubusercontent.com/33985509/127531882-4f87a6be-1c78-4450-884b-26cbc5f4c5cf.png)


![image](https://user-images.githubusercontent.com/33985509/127532556-3181b33f-fbe6-423c-b4cc-27f8147f5827.png)


![image](https://user-images.githubusercontent.com/33985509/127533133-c587547a-b482-4081-a26b-1e99e7367c15.png)


![image](https://user-images.githubusercontent.com/33985509/127533534-a3dd216a-4de5-4130-a04c-cbb2d6513c92.png)


![image](https://user-images.githubusercontent.com/33985509/127533821-6f25284c-aa14-459c-8301-fbd395911139.png)


![image](https://user-images.githubusercontent.com/33985509/127533974-b49404db-f04d-41ad-9cc6-6c02f41a1b01.png)


![image](https://user-images.githubusercontent.com/33985509/127534254-e08c9c4b-fe1b-4dd1-ad3a-e41a9021577c.png)


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
