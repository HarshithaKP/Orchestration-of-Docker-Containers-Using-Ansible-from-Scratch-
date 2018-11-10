
Orchestration of Containers Using Ansible from Scratch

Steps for installing Ansible:on Contoller 

	$ sudo apt-get update 

	$sudo apt-get install python3-pip 

	$sudo apt-get install software-properties-common 

	$sudo -E apt-add-repository --yes --update ppa:ansible/ansible 

	$sudo apt-get install ansible 

	$ansible --version ( To check installed ansible version) 


Methodology: 


After installing Ansible on Linux 

Step 1:  Build a docker image with Dockerfile(To create Nginx and Apache2 containers) 

First, create a directory on the workstation and a Dockerfile within the created directory. 

$mkdir docker 
$cd docker 
$touch Dockerfile 

Edit Dockerfile with nano and add the following content: 

# Version: 0.0.1 

FROM Ubuntu:latest 
RUN apt-get update 
RUN apt-get install -y nginx 
RUN echo 'Default page. Nginx is in your container. ' \ 
>/usr/share/nginx/html/index.html 
EXPOSE 80 


Step 2:  Edit inventory file 

Inventory file contains IP addresses or domain names where we want deploy container. Add this file in your project: 
$touch ../hosts 

Edit the hosts file with nano and add the following content within this file. 

[webserver] 
your_server_ip 

Now, check if your host machine can communicate with the nodes via Ansible. Type the following command in terminal: 

$ansible webserver -m ping -i ../hosts 

Step 3 : Edit Ansible playbook(main.yml) 

playbook will have ansible code for the reccomended process. 

First, change the working directory to the project root directory and create a new Ansible playbook. The directory layout should look like: 

docker_project/ 
   main.yml 
   hosts 
   docker/ 
       Dockerfile 


Step 4 : Running the playbook 

Run the playbook by using the following command on host:	 

$ansible-playbook -i ~/hosts main.yml --ask-become-pass -ask-sudo-pass --ask-pass 


Checking the Running containers from host: 

In the host browser type the node ip with port exposed for Nginx/Apache 


