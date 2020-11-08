

# k3s

https://k3s.io/


K3s is officially supported and tested on the following operating systems and their subsequent non-major releases:

Ubuntu 16.04 (amd64)
Ubuntu 18.04 (amd64)
Raspbian Buster*

Hardware requirements scale based on the size of your deployments. Minimum recommendations are outlined here.

RAM: 512MB Minimum (we recommend at least 1GB)
CPU: 1 Minimum

![image](https://user-images.githubusercontent.com/33985509/98454261-e22c5580-2162-11eb-95f2-ba5d4ec0a0e3.png)



# AWS Freertos

https://aws.amazon.com/freertos/


# Aws Greengrass

https://aws.amazon.com/greengrass/


# AWS Iot Policies

https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html


# Mqtt protocol

https://mqtt.org/

```
1.Publish/Subscribe
2.Messages
3.Topics
4.Broker

```


# Reference screen prints :


![image](https://user-images.githubusercontent.com/33985509/98452431-97551280-214f-11eb-84a5-d38d3a4620de.png)


![image](https://user-images.githubusercontent.com/33985509/98452436-a50a9800-214f-11eb-97dc-d8b3598f11a7.png)


![image](https://user-images.githubusercontent.com/33985509/98452424-860c0600-214f-11eb-866c-826159abfd28.png)


![image](https://user-images.githubusercontent.com/33985509/98452417-7a204400-214f-11eb-89e3-5f103ca7b2ee.png)


![image](https://user-images.githubusercontent.com/33985509/98452412-6aa0fb00-214f-11eb-91dd-616fe22fdc36.png)


![image](https://user-images.githubusercontent.com/33985509/98452449-c075a300-214f-11eb-9984-f10aa0476872.png)


![image](https://user-images.githubusercontent.com/33985509/98452458-d8e5bd80-214f-11eb-8bb8-e7c15bc6d0c9.png)


![image](https://user-images.githubusercontent.com/33985509/98452461-e4d17f80-214f-11eb-968a-2f0773d370c9.png)


![image](https://user-images.githubusercontent.com/33985509/98452486-19ddd200-2150-11eb-9434-e31252e58742.png)





# Ec2

![image](https://user-images.githubusercontent.com/33985509/98452583-e51e4a80-2150-11eb-9764-b5ee34fc6e66.png)

![image](https://user-images.githubusercontent.com/33985509/98452594-fb2c0b00-2150-11eb-90ac-9b645e4f921d.png)

![image](https://user-images.githubusercontent.com/33985509/98452720-1ea38580-2152-11eb-8604-3ebb23811d98.png)

# RDS

![image](https://user-images.githubusercontent.com/33985509/98452742-51e61480-2152-11eb-8534-7976c8f9bcea.png)


![image](https://user-images.githubusercontent.com/33985509/98452769-7f32c280-2152-11eb-9042-cd4da8767aed.png)


VPC is default and autoscaling off


# Steps


Go to k3s-master

apt update -y

apt upgrade -y

apt install mysql-client -y


copy the rds endpoint name and give as below in k3s-master

mysql -h k3sdb.cc5prv9jqd9.us-east-1.rds.amazonaws.com -u k3s -p

and enter sql password


show databases;

create DATABASE k3s;

* K3S_DATASTORE_ENDPOINT = Specify a PostgresSQL, MySQL, or etcd connection string. This is a string used to describe the connection to the datastore. The structure of this string is specific to each backend and is detailed below.


export K3S_DATASTORE_ENDPOINT='mysql://k3s:password@tcp(k3sdb.cc5prv9jqd9.us-east-1.rds.amazonaws.com:3306)/k3s'

By default it write the below

* --write-kubeconfig value, -o value         (client) Write kubeconfig for admin client to this file [$K3S_KUBECONFIG_OUTPUT]

* --write-kubeconfig-mode value              (client) Write kubeconfig with this mode [$K3S_KUBECONFIG_MODE]



curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--write-kubeconfig=/opt/.kube/config --write-kubeconfig-mode=644" sh -

systemctl status k3s

kubectl get nodes

sudo -i

kubectl get ns

kubectl get pods -n kube-system

cd /var/lib/rancher

cd k3s

cd server

cat token

xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:server:xxxxxxxxxxxxxxxxxxxxx

Got to worker nodes(k3s-worker01, k3s-worker02, k3s-worker03 )


sudo -i

export K3S_URL=https://172.10.12.23:6443 (this was the private ip of k3s-master)


export K3S_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx:server:xxxxxxxxxxxxxxxxxxxxx

curl -sfL https://get.k3s.io | sh -

Systemctl status k3s-agent

go to k3s-master 

mysql -h k3sdb.cc5prv9jqd9.us-east-1.rds.amazonaws.com -u k3s -p

and enter sql password


use k3s;

show tables;

