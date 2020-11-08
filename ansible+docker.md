



touch myhosts.txt

vim myhosts.txt

```

[ProductionInstances]
10.0.1.16 ansible_ssh_user=root ansible_ssh_pass=Welcome@123
10.0.2.16 ansible_ssh_user=root ansible_ssh_pass=Welcome@123
10.0.3.16 ansible_ssh_user=root ansible_ssh_pass=Welcome@123

```



/etc/ansible/ansible.cfg

```

[defaults]
inventory = /root/home/myhosts.txt
ansible_host_key_checking=FALSE

```

- hosts: "ProductionInstances"
  tasks: 
   - name: Configuring Docker Repository
     yum_repository:
       name: Docker
       description: "Docker Repo"
       baseurl: "https://download.docker.com/linux/centos/docker-ce.repo" 
       gpgcheck: no
     register: x

   - name: Checking Configuration Status
     debug:
       var: x.failed

   - name: Installing Docker
     package:
       name: "docker-ce-18.06.3.ce-3.el7.x86_64"
       state: present
     register: y

   - name: Checking Install Status
     debug:
       var: y.failed

   - name: Starting Docker Daemon
     service:
       name: docker
       state: started
       enabled: yes
     when: y.failed == false

   - name: Install
     command: "pip install docker-py"    

   - name: Pull a Docker Image
     docker_image: 
        name: httpd
        tag: latest
        source: pull
     register: z
   - name: Checking Pull Status
     debug: 
       var: z

   - name: Creating a Persistent Volume Dir
     file:
       path: "/root/pv"
       state: directory

   - name: Copying the HTML code in the Directory
     copy: 
       src: "/root/Desktop/index.html"
       dest: "/root/pv"

   - name: Launching an HTTPD Container
     when: z.failed == false
     docker_container:
       name: apache-server
       image: httpd
       state: started
       exposed_ports:
         - "80"
       ports:
         - "8888:80"
       volumes: 
         - /root/pv:/usr/local/apache2/htdocs
