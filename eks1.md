![image](https://user-images.githubusercontent.com/33985509/101885324-48f5c200-3b9a-11eb-8189-f67eab5a67ca.png)

![image](https://user-images.githubusercontent.com/33985509/101885454-6e82cb80-3b9a-11eb-95de-a236fb7b7a9b.png)

AKIAXOBQPVJN352WUJ75

6E/76lDV5CB+m4C52BDSsZKOsgBYVEFtt/Ix9nHi


![image](https://user-images.githubusercontent.com/33985509/101885788-e0f3ab80-3b9a-11eb-8873-e2f0593230b0.png)


![image](https://user-images.githubusercontent.com/33985509/101885845-f1a42180-3b9a-11eb-8262-29284aac82ff.png)


![image](https://user-images.githubusercontent.com/33985509/101886111-53fd2200-3b9b-11eb-8caa-afb06cfd5b69.png)


![image](https://user-images.githubusercontent.com/33985509/101886151-65dec500-3b9b-11eb-97be-5108cab38e08.png)


aws-cli/2.1.10 Python/3.7.3 Linux/4.14.203-156.332.amzn2.x86_64 exe/x86_64.amzn.2 prompt/off




eksctl --version  0.34.0

kubectl version --short --client
Client Version: v1.16.8-eks-e16311

![image](https://user-images.githubusercontent.com/33985509/101895336-b3612f00-3ba7-11eb-9dd3-fa455007cf38.png)


![image](https://user-images.githubusercontent.com/33985509/101895435-d12e9400-3ba7-11eb-816e-d1a558feb9f4.png)





Steps





aws --version

apt install awscli -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

which aws

sudo ./aws/install --bin-dir /usr/bin --install-dir /usr/bin/aws-cli --update

aws --version

![image](https://user-images.githubusercontent.com/33985509/101992777-f27da600-3cb5-11eb-89a8-2f23b2826f2b.png)

aws configure

For AWS Access Key ID, paste in the access key ID you copied earlier.

For AWS Secret Access Key, paste in the secret access key you copied earlier.

For Default region name, enter us-east-1.

For Default output format, enter json.

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/linux/amd64/kubectl


chmod +x ./kubectl

mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

kubectl version --short --client

![image](https://user-images.githubusercontent.com/33985509/101992821-3c668c00-3cb6-11eb-875c-f486c0c61607.png)

curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp

sudo mv /tmp/eksctl /usr/bin

eksctl version

![image](https://user-images.githubusercontent.com/33985509/101992846-57390080-3cb6-11eb-8560-4ea970d451e6.png)



touch nginx-svc.yaml

vi nginx-svc.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  labels:
    env: dev
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    env: dev

```




touch nginx-deployment.yaml

vi nginx-deployment.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    env: dev
spec:
  replicas: 3
  selector:
    matchLabels:
      env: dev
  template:
    metadata:
      labels:
        env: dev
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80


```


eksctl create cluster --name dev --version 1.16 --region us-east-1 --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed

![image](https://user-images.githubusercontent.com/33985509/101993460-4343cd80-3cbb-11eb-8502-54bde0fc9a1e.png)



eksctl get cluster

aws eks update-kubeconfig --name dev --region us-east-1

sudo yum install -y git

cat nginx-deployment.yaml

cat nginx-svc.yaml

kubectl apply -f ./nginx-svc.yaml

kubectl get service

kubectl apply -f ./nginx-deployment.yaml


curl "<LOAD_BALANCER_EXTERNAL_IP>"

kubectl get deployment

kubectl get pod

kubectl get rs

kubectl get node

select the three t3.micro instances.

Click Actions > Instance State > Stop.

kubectl get node

kubectl get pod

kubectl get node

eksctl delete cluster

kubectl get service

curl "<LOAD_BALANCER_EXTERNAL_IP>"
