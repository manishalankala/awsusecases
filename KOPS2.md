

# VPC

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

# Attach Internet gateway to vpc

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

aws ec2 create-subnet --vpc-id <VPC_ID> --cidr-block <CIDR_BLOCK> --availability-zone <AVAILABILITY_ZONE> --region eu-west-1


# Configure NAT Gateway

create 3 NAT Gateways. Since these NAT Gateways should connect to the public Internet, also need to allocate 3 Elastic IPs

aws ec2 allocate-address --domain vpc --region eu-west-1

Use the AllocationId to create the NAT Gateway for the public zone in eu-west-1a

aws ec2 create-nat-gateway --subnet-id <SUBNET_ID> --allocation-id <ALLOCATION_ID> --region eu-west-1


# Configure the Route Tables

Route Table for the 3 public zones

We can join the routes for the three public subnets in one Route Table and then associate the three public subnets to this Route Table

Public Route Table

aws ec2 create-route-table --vpc-id <VPC_ID> --region eu-west-1

create a route for the Internet Gateway

aws ec2 create-route --route-table-id <ROUTE_TABLE_ID> --destination-cidr-block 0.0.0.0/0 --gateway-id <INTERNET_GATEWAY_ID> --region eu-west-1

associate our public subnets with the Route Table

aws ec2 associate-route-table --route-table-id <ROUTE_TABLE_ID> --subnet-id <SUBNET_ID> --region eu-west-1

# Private Route Tables

aws ec2 create-route-table --vpc-id <VPC_ID> --region eu-west-1

Create the route that points to our NAT Gateway.

aws ec2 create-route --route-table-id <ROUTE_TABLE_ID> --destination-cidr-block 0.0.0.0/0 --nat-gateway-id <NAT_GATEWAY_ID> --region eu-west-1

Associate the subnet

aws ec2 associate-route-table --route-table-id <ROUTE_TABLE_ID> --subnet-id <SUBNET_ID> --region eu-west-1

Setting up DNS in AWS Route53

I had already configured my AWS Route53 with my domain as a public hosted zone. 

need to set up a public hosted zone with your domain, and have your provider point to AWS DNS name servers. 

You can verify that this is the case by calling the following, and verify that the AWS DNS nameservers are responding.


# Create an S3 Bucket as Kops state store

aws s3api create-bucket --bucket kubecloud-state-store --region eu-west-1
 Also have to set up a private hosted zone for your domain. Again, this was already setup in my account.

The easy way to do this is by going to the Route53 in the web-console. 

Press Create Hosted Zone, enter the same domain as the public zone, and choose the type to be private and associate your VPC from the dropdown-list

Installing Kops

Verify that the version is installed correctly

# Create the HA Cluster with Kops

export NAME=<CLUSTER_NAME> export KOPS_STATE_STORE=s3://<BUCKET_NAME> export VPC_ID=<VPC_ID> export DNS_ZONE_PRIVATE_ID=<ID_OF_PRIVATE_HOSTED_ZONE>

kops create cluster \ --node-count 3 \ --zones eu-west-1a,eu-west-1b,eu-west-1c \ --master-zones eu-west-1a,eu-west-1b,eu-west-1c \ --dns-zone=${DNS_ZONE_PRIVATE_ID} \ --dns private \ --node-size t2.medium \ --master-size t2.small \ --topology private \ --networking weave \ --vpc=${VPC_ID} \ --bastion \ ${NAME}


--dns-zones the id of the private zone to use

--node-count defines the number of nodes

--dns private defines that we want to use a private hosted zone.

--node-size and --master-size defines the instance types we want yo use.

--topology private specifies that we want our nodes to be in the private subnets.

--networking weave defines the network to be used

--vpc the vpc id to use.

--bastion tells Kops that we want a bastion jump server in our cluster.

Edit the cluster

kops edit cluster ${NAME}

Change subnet configuration

subnets: - id: subnet-0e89f256 egress: nat-0b80a9c336c8e4e4b name: eu-west-1a type: Private zone: eu-west-1a - id: subnet-c3320ca7 egress: nat-0eed67fdd1d1a2b72 name: eu-west-1b type: Private zone: eu-west-1b - id: subnet-c09dafb6 egress: nat-0c297125cb75a6995 name: eu-west-1c type: Private zone: eu-west-1c - id: subnet-4d89f215 name: utility-eu-west-1a type: Utility zone: eu-west-1a - id: subnet-e4320c80 name: utility-eu-west-1b type: Utility zone: eu-west-1b - id: subnet-e09daf96 name: utility-eu-west-1c type: Utility zone: eu-west-1c

kops update cluster ${NAME} --yes

the cluster will only be accessible from within AWS

kops update cluster ${NAME}
