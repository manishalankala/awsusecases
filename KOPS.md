

![image](https://user-images.githubusercontent.com/33985509/98471424-5b23bf80-21ec-11eb-9dda-6c8b6ffa3871.png)



# Required 

```
aws access

awscli

kops

Ec2
Ubuntu instance

Roles:
AmazonSSMFullAccess

AmazonRoute53DomainsFullAccess

AmazonRoute53AutoNamingFullAccess



```




# Python

```
sudo apt update
sudo apt -y install python3-pip

sudo apt-get update
sudo apt-get -y install python-pip


sudo pip3 install --upgrade pip
sudo pip install --upgrade pip

```



# Awscli

```
sudo apt-get update

sudo apt-get install awscli

aws --version


or 


using PIP

sudo pip install awscli
sudo pip3 install awscli

```


Install Kubectl on Linux


```

curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl

```

# kops

```
wget https://github.com/kubernetes/kops/releases/download/1.6.1/kops-linux-amd64
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops

```

# Route53

role to access S3 and Route53

Create a hosted zone on Route53, say, k8s.application.vpc. The API server endpoint will then be api.k8s.application.vpc



# S3 bucket

aws s3 mb s3://clusters.k8s.application.vpc

export KOPS_STATE_STORE=s3://clusters.k8s.application.vpc


# Kubernetes Cluster

kops create cluster --cloud=aws --zones=us-east-1d --name=useast1.k8s.application.vpc --dns-zone=application.vpc --dns private

*Be sure you have ssh keys already generated otherwise it will throw an error

kops update cluster useast1.k8s.application.vpc --yes

* Without –yes option, it will print the action it is going to perform without actually doing it.


List clusters with-  kops get cluster

Edit this cluster with - kops edit cluster useast1.k8s.appychip.vpc

Edit your node instance group: kops edit ig --name=useast1.k8s.application.vpc nodes

Edit your master instance group: kops edit ig --name=useast1.k8s.application.vpc master-us-east-1d

kubectl get nodes

Enable UI

kubectl create -f https://rawgit.com/kubernetes/dashboard/master/src/deploy/kubernetes-dashboard.yaml

kubectl proxy --port=8080 &

To deploy nginx

kubectl run sample-nginx --image=nginx --replicas=2 --port=80

kubectl get pods

kubectl get deployments

kubectl expose deployment sample-nginx --port=80 --type=LoadBalancer

kubectl get services -o wide

copy the elb url and test in browser

master node’s IP/Domain in browser

kubectl config view
