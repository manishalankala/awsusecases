


Instance1: devserver

Instance2: jenkinsserver

check the git version and maven version if installed

manage Jenkins ---> System configuration

![image](https://user-images.githubusercontent.com/33985509/98478098-0afe2a80-21f7-11eb-8be2-d9b06612e470.png)

![image](https://user-images.githubusercontent.com/33985509/98479070-5c0e1e80-21f7-11eb-994e-c34b03c0f04a.png)


# Configure ansible

sudo apt-get update

sudo apt-get upgrade -y

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
