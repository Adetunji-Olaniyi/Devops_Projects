Automate User Creation on Linux Server using Ansible
Introduction
Managing user accounts is a common administrative task for Linux servers. Manually creating and managing user accounts can become tedious, especially on multiple servers. Ansible simplifies this process by automating user creation with playbooks. This project will guide us in creating an Ansible playbook to automate user creation on a Linux server.

Objectives
Understand the basics of Ansible and its automation capabilities.
Set up an Ansible environment to manage Linux servers.
Create an Ansible playbook to automate user creation.
Configure additional settings like home directory, groups, and SSH access.
Verify the user creation process and test access.
Prerequisites
Linux Servers: At least one Linux server to act as the target machine and an optional control machine for Ansible.
Ansible Installed: Ansible installed on the control machine. (Refer to the Ansible installation guide if you don't have Ansible already installed.) https://docs.ansible.com/projects/ansible/latest/installation_guide/intro_installation.html
SSH Access: SSH access between the control machine and target servers with public key authentication.
Tools: A text editor to create and edit Ansible playbooks.
Tasks Outline
Install and configure Ansible on the control machine.
Set up an inventory file for the target Linux server.
Create an Ansible playbook to automate user creation.
Configure additional user settings like groups and SSH access.
Verify user creation and test login.
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

ssh ubuntu@98.93.9.134

keygen addkeytoNode logintoNodeServer

We have now successfully configured a passwordless SSH access.

Task 2 - Set Up the Ansible Inventory File
Create a directory for Ansible configuration:

mkdir ~/ansible cd ~/ansible

AnsibleFile

Create an inventory file:

vim inventory.ini

inventoryfile

Add target machine details to the inventory:

[linux_servers]

target1 ansible_host=98.93.9.134 ansible_user=ubuntu

AnsibleTarget

Save and close the file.

Task 3 - Create an Ansible Playbook to Automate User Creation
Create a playbook file for user creation:

vim create_users.yml

UserCreation

Add the following playbook content:

Playbook Userplaybook Playbookaddee

Task 4: Configure Additional User Settings
Update the playbook to include group and SSH key configuration:

Replace /path/to/user1.pub and /path/to/user2.pub with the paths to the public SSH keys for each user.

Playbook

AnsiblePalybook

AnsiblePlaybook

Task 5 - Verify User Creation and Test Login
Run the playbook to create users:

ansible-playbook -i inventory.ini create_users.yml

Usercreated

Verify the users were created on the target server:

cat /etc/passwd

etc

ls /home

lshome

Test SSH access for the newly created users:

ssh user1@<target-server-ip>

ssh user1@98.93.9.134

sshuserone

ssh user2@<target-server-ip>

ssh user2@54.146.240.78

sshusertwo

Conclusion
In this project, we automated the creation of user accounts on a Linux server using Ansible. We learned how to write an Ansible playbook for user creation, configure additional settings like groups and SSH access, and verify the process. With these skills, you can manage user accounts efficiently across multiple servers and extend the playbook for advanced configurations like password policies and user deletion.

END.