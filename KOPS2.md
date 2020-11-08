

Create VPC

VPC with a CIDR block - 10.0.0.0/16


nodes to be placed on a private network without any Public IPs 

(don’t want our instances to be reachable from the public internet)


Have to create 3 NAT Gateway nodes one for each private zone.

(The NAT Gateway allows private instances to communicate with the internet)


If you have multiple keys defined for the awscli tool in ~/.aws/credentials, set the profile for the AWS account you want to use.

export AWS_DEFAULT_PROFILE=k8s_private or or, just run the aws configure.


aws ec2 create-vpc --cidr-block 10.0.0.0/16 --region eu-west-1 { "Vpc": { "VpcId": "vpc-a55e77c1", "InstanceTenancy": "default", "Tags": [], "State": "pending", "DhcpOptionsId": "dopt-b8ee9cdd", "CidrBlock": "10.0.0.0/16", "IsDefault": false } }

Modify the VPC to allow DNS hostnames by running the following command:

aws ec2 modify-vpc-attribute --vpc-id <VPC_ID> --enable-dns-hostnames "{\"Value\":true}" --region eu-west-1

# Internet gateway

aws ec2 create-internet-gateway --region eu-west-1

# Attach internet gateway to vpc

aws ec2 attach-internet-gateway --internet-gateway-id <INTERNET_GATEWAY_ID> --vpc-id <VPC_ID> --region eu-west-1


3 public subnets and 3 private subnets. a public and private subnet in each Availability Zone


# Public subnets

10.0.0.0/20 for the subnet in eu-west-1a

10.0.16.0/20 for the subnet in eu-west-1b

10.0.32.0/20 for the subnet in eu-west-1c

aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block <CIDR_BLOCK> --availability-zone <AVAILABILITY_ZONE> --region eu-west-1

aws ec2 modify-subnet-attribute --subnet-id <SUBNET_ID> --map-public-ip-on-launch --region eu-west-1 (public subnets to auto-assign public ip to instances.)


# Private Subnets

10.0.48.0/20 for eu-west-1a

10.0.64.0/20 for eu-west-1b

10.0.80.0/20 for eu-west-1c
