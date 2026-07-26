Deploy and Configure Nginx Web Server using Ansible
Introduction
Nginx is a powerful and widely used web server known for its performance and flexibility. Deploying and configuring Nginx manually on multiple servers can be time-consuming, but with Ansible, this process becomes automated and efficient. This project will teach us how to use Ansible to deploy and configure an Nginx web server on a Linux machine.

Objectives
Understand how Ansible simplifies the deployment and configuration of applications.
Set up an Ansible environment for managing Linux servers.
Create and execute an Ansible playbook to install Nginx.
Configure a basic Nginx website using Ansible. Verify the Nginx deployment.
Prerequisites
Linux Servers: At least one server to act as the target machine and an optional control machine for Ansible.
Ansible Installed: Ansible installed on the control machine. (Refer to the Ansible installation guide if needed.)
SSH Access: SSH access between the control machine and target servers with public key authentication.
Tools: A text editor to create and edit Ansible playbooks.
Tasks Outline
Install and configure Ansible on the control machine.
Set up an inventory file for the target Linux server.
Create an Ansible playbook to install Nginx. Configure a custom Nginx website using Ansible.
Verify the Nginx deployment and access the website.
Project Tasks
Task 1 - Install and Configure Ansible
Install Ansible on the control machine (Ubuntu example):
On this project, I will be using Ubuntu created on AWS and login to the ubuntu Linux server.

AnsibleonAWS

Login to the ubuntu server and update.

Update the package repository

sudo apt update

aptupdate

Install Ansible:

sudo apt install ansible -y

InstallAnsible

Verify the installation:

ansible --version

The output should display the installed Ansible version like this:

VerifyAnsible

Set up SSH key-based authentication between the control machine and target server:

Follow the steps below to generate keygen on the controller machine, copy the key to the Node server and access the Node server from the controller machine as below:

Login to access the controller server on AWS

cd ~/.ssh

 ls

ssh-keygen # this will generate the public id and private id

cat id_ed25519.pub #This would show the public id

Copy the public ID to the server you wanted to manage

Test SSH access without a password:

ssh ubuntu@54.221.50.28

keygen

addkeytoNode

AccessNode1Server

We have now successfully configured a passwordless SSH access.

Task 2 - Set Up the Ansible Inventory File
Create a directory for Ansible configuration:

mkdir ~/ansible cd ~/ansible

AnsibleFile

Create an inventory file:

vim inventory.ini

inventoryfile

Add target machine details to the inventory:

[web_servers] target ansible_host=54.221.50.28 ansible_user=ubuntu

AnsibleTarget

Save and close the file.

Task 3 - Create an Ansible Playbook to Install Nginx
Create a playbook file for installing Nginx:

vim install_nginx.yml

Createnginxfile

Add the following playbook content:

nginxfile

nginxfile

Save the file.

Task 4 - Configure a Custom Nginx Website Using Ansible
Create a playbook for Nginx website configuration:

vim configure_nginx.yml

ConfigureNginc

Add the following playbook content:

ConfigFile

ConfigFileAddded ConfigFileAdded

Task 5 - Verify the Nginx Deployment
Run the playbooks to install and configure Nginx:

ansible-playbook -i inventory.ini install_nginx.yml

NginxInstalled

ansible-playbook -i inventory.ini configure_nginx.yml

NginxDeployed

Verify Nginx is running on the target server:

Edit securiy group in AWS to allow inbound rulles to application access.

SGAccess

curl http://<target-server-ip>

curl http://54.221.50.28

WebAccess

Open the target server's IP address in a web browser to access the custom website.

WebAccess

Conclusion
In this project, we used Ansible to automate the deployment and configuration of the Nginx web server on a Linux machine. we created reusable playbooks for installing Nginx and deploying a custom website. With these skills, we can manage multiple web servers efficiently, customize configurations further, and scale your deployment processes.

END.