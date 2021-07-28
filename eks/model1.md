

IAM User with Admin Permissions + add users


![image](https://user-images.githubusercontent.com/33985509/127368453-4438382c-3776-4ff1-bcc4-e3bd39db3dff.png)


![image](https://user-images.githubusercontent.com/33985509/127368517-a5756d02-4773-4fac-b57b-3b12f183130c.png)


![image](https://user-images.githubusercontent.com/33985509/127368654-305c810b-5a64-45db-af4f-ec9b124d7f28.png)


![image](https://user-images.githubusercontent.com/33985509/127368741-989a5183-4728-493b-a9fe-9eb2ecdd81c6.png)


AKIA2ICVEGXSPBMYPNHI 

AKIA2ICVEGXSI67A3UEQ

AKIA2ICVEGXSBPPLKWNG - k8s-admin


AKIA2ICVEGXSB4A5MZP3 - k8s-admin2


aws configure

EC2 Instance and Configuring the Command Line Tools

launch an ami instance of free tier t2micro 

aws --version

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install --bin-dir /usr/bin --install-dir /usr/bin/aws-cli --update




Configure the CLI:

aws configure

For AWS Access Key ID, paste in the access key ID you copied earlier.

For AWS Secret Access Key, paste in the secret access key you copied earlier.

For Default region name, enter us-east-1.

For Default output format, enter json.







https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl

chmod +x ./kubectl


mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

kubectl version --short --client

https://github.com/weaveworks/eksctl

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/bin

eksctl version

kubectl version --short --client

eksctl version = 0.58.0

kubectl version --short --client =  v1.19.6-eks-49a6c0

eksctl create cluster --name dev --version 1.19 --region us-east-1 --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed


eksctl utils describe-stacks --region=us-east-1 --cluster=dev'

eksctl get cluster

aws eks update-kubeconfig --name dev --region us-east-1

sudo yum install -y git

git clone https://github.com/ACloudGuru-Resources/Course_EKS-Basics

cd Course_EKS-Basics

cat nginx-deployment.yaml

cat nginx-svc.yaml

kubectl apply -f ./nginx-svc.yaml

kubectl get service

kubectl apply -f ./nginx-deployment.yaml

kubectl get deployment

kubectl get pod

kubectl get rs

kubectl get node

curl "<LOAD_BALANCER_EXTERNAL_IP>"


kubectl get node

kubectl get pod

kubectl get node

kubectl get pod

kubectl get service

curl "<LOAD_BALANCER_EXTERNAL_IP>"

eksctl delete cluster dev




~~~

aws --version
It should be an older version.

Download v2:

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
Unzip the file:

unzip awscliv2.zip
See where the current AWS CLI is installed:

which aws
It should be /usr/bin/aws.

Update it:

sudo ./aws/install --bin-dir /usr/bin --install-dir /usr/bin/aws-cli --update
Check the version of AWS CLI:

aws --version
It should now be updated.

Configure the CLI:

aws configure
For AWS Access Key ID, paste in the access key ID you copied earlier.

For AWS Secret Access Key, paste in the secret access key you copied earlier.

For Default region name, enter us-east-1.

For Default output format, enter json.

Download kubectl:

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/linux/amd64/kubectl
Apply execute permissions to the binary:

chmod +x ./kubectl
Copy the binary to a directory in your path:

mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
Ensure kubectl is installed:

kubectl version --short --client
Download eksctl:

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
Move the extracted binary to /usr/bin:

sudo mv /tmp/eksctl /usr/bin
Get the version of eksctl:

eksctl version
See the options with eksctl:

eksctl help
Provision an EKS Cluster
Provision an EKS cluster with three worker nodes in us-east-1:

eksctl create cluster --name dev --version 1.16 --region us-east-1 --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed
It will take 10–15 minutes since it's provisioning the control plane and worker nodes, attaching the worker nodes to the control plane, and creating the VPC, security group, and Auto Scaling group.

In the AWS Management Console, navigate to CloudFormation and take a look at what’s going on there.

Select the eksctl-dev-cluster stack (this is our control plane).

Click Events, so you can see all the resources that are being created.

We should then see another new stack being created — this one is our node group.

Once both stacks are complete, navigate to Elastic Kubernetes Service > Clusters.

Click the listed cluster.

Click the Compute tab, and then click the listed node group. There, we'll see the Kubernetes version, instance type, status, etc.

Click dev in the breadcrumb navigation link at the top of the screen.

Click the Networking tab, where we'll see the VPC, subnets, etc.

Click the Logging tab, where we'll see the control plane logging info.

The control plane is abstracted — we can only interact with it using the command line utilities or the console. It’s not an EC2 instance we can log into and start running Linux commands on.
Navigate to EC2 > Instances, where you should see the instances have been launched.

Close out of the existing CLI window, if you still have it open.

Select the original t2.micro instance, and click Connect at the top of the window.

In the Connect to your instance dialog, select EC2 Instance Connect (browser-based SSH connection).

Click Connect.

In the CLI, check the cluster:

eksctl get cluster
Enable it to connect to our cluster:

aws eks update-kubeconfig --name dev --region us-east-1
Create a Deployment on Your EKS Cluster
Install Git:

sudo yum install -y git
Download the course files:

git clone https://github.com/ACloudGuru-Resources/Course_EKS-Basics
Change directory:

cd Course_EKS-Basics
Take a look at the deployment file:

cat nginx-deployment.yaml
Take a look at the service file:

cat nginx-svc.yaml
Create the service:

kubectl apply -f ./nginx-svc.yaml
Check its status:

kubectl get service
Copy the external IP of the load balancer, and paste it into a text file, as we'll need it in a minute.

Create the deployment:

kubectl apply -f ./nginx-deployment.yaml
Check its status:

kubectl get deployment
View the pods:

kubectl get pod
View the ReplicaSets:

kubectl get rs
View the nodes:

kubectl get node
Access the application using the load balancer, replacing <LOAD_BALANCER_EXTERNAL_IP> with the IP you copied earlier:

curl "<LOAD_BALANCER_EXTERNAL_IP>"
The output should be the HTML for a default Nginx web page.

In a new browser tab, navigate to the same IP, where we should then see the same Nginx web page.

Test the High Availability Features of Your EKS Cluster
In the AWS console, on the EC2 instances page, select the three t3.micro instances.

Click Actions > Instance State > Stop.

In the dialog, click Yes, Stop.

After a few minutes, we should see EKS launching new instances to keep our service running.

In the CLI, check the status of our nodes:

kubectl get node


~~~
