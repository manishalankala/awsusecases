

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

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/bin

eksctl version = 0.58.0

kubectl version --short --client =  v1.19.6-eks-49a6c0

eksctl create cluster --name dev --version 1.19 --region us-east-1 --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed



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
