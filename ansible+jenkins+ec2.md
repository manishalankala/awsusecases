


Instance1: devserver

Instance2: jenkinsserver

check the git version and maven version if installed

manage Jenkins ---> System configuration

![image](https://user-images.githubusercontent.com/33985509/98478098-0afe2a80-21f7-11eb-8be2-d9b06612e470.png)

![image](https://user-images.githubusercontent.com/33985509/98479070-5c0e1e80-21f7-11eb-994e-c34b03c0f04a.png)


# Configure ansible

sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get docker -y

usermod -aG docker jenkins

sudo apt-get install python -y

sudo apt install ansible -y or sudo amazon-linux-extras install ansible2

ansible --version

config file = /etc/ansible/ansible.cfg

executable location = /usr/bin/ansible

ansible python module location = /usr/lib/python /site-packages/ansible

Go to Manage jenkins ----> Manage Plugins

![image](https://user-images.githubusercontent.com/33985509/98481285-7cd77380-21f9-11eb-852a-500a80aee3c4.png)

![image](https://user-images.githubusercontent.com/33985509/98481311-ad1f1200-21f9-11eb-9f57-9236734ec38e.png)


install without restart

Go to Manage Jenkins ---> Global configuration

![image](https://user-images.githubusercontent.com/33985509/98481375-09823180-21fa-11eb-8b82-4013e7927960.png)


Go to create item --->name docker-ansible --> pipeline project 

![image](https://user-images.githubusercontent.com/33985509/98481540-4d296b00-21fb-11eb-8701-29dcb7d7fdda.png)

![image](https://user-images.githubusercontent.com/33985509/98481603-aabdb780-21fb-11eb-8dff-15ea0438e1e2.png)

![image](https://user-images.githubusercontent.com/33985509/98481626-d771cf00-21fb-11eb-83b7-860aa77f059f.png)

so here we are adding the credentials linking jenkins to access github

click generate pipeline script

![image](https://user-images.githubusercontent.com/33985509/98481710-67b01400-21fc-11eb-9b7e-75655792ed3f.png)

Build now

if we get maven command not found

the go to pipeline syntax then  Declarative Directive generator


![image](https://user-images.githubusercontent.com/33985509/98481909-02f5b900-21fe-11eb-8a1d-a3f5e4e6dac4.png)


add as maven

click generate Declarative Directive 

add this below under pipeline script  under agent any

tools {
 maven 'maven3'
}



Now we try to add one more stage in script

stage('Docker Build'){
     steps{
         sh "docker build . -t manishalankala/app:0.0.1 ." or sh "docker build . -t manishalankala/app:${DOCKER_TAG}"
      }
 }
 
 def getVersion(){
     def commitHash = sh label: '',returnStdout: true,script:'git rev-parse --short HEAD'
     return commitHash
 }
 



![image](https://user-images.githubusercontent.com/33985509/98482089-2bca7e00-21ff-11eb-9e72-ebc4a1823459.png)

check disable host ssh key check

![image](https://user-images.githubusercontent.com/33985509/98482156-c3c86780-21ff-11eb-9fb5-716663bcfbcb.png)

environment {
    Docker_TAG = "getversion()"
}


service jenkins restart

service docker restart




ansible Playbook file

deploydocker.yml

```
---
- hosts: dev
  become: True
  tasks:
    - name: Install python pip
      yum:
        name: python-pip
        state: present
    - name: Install docker
      yum:
        name: docker
        state: present
    - name: start docker
      service:
        name: docker
        state: started
        enabled: yes
    - name: Install docker-py python module
      pip:
        name: docker-py
        state: present
    - name: Start the container
      docker_container:
        name: hariapp
        image: "nodejscn/node:{{DOCKER_TAG}}"
        state: started
        published_ports:
          - 0.0.0.0:8080:8080
          
```

Create inventory file

deployinventory.ini

[dev]
172.31.34.192 ansible_user=ec2-user


run the build job



open browser ip:8080/jenkinsitemname


![image](https://user-images.githubusercontent.com/33985509/98485490-11040380-2217-11eb-925c-850d3ddd2091.png)


![image](https://user-images.githubusercontent.com/33985509/98485474-e7e37300-2216-11eb-93ec-5e6734ff7403.png)
