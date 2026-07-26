Backup and Restore Files on a Linux Server using Ansible
Introduction
Data backup and restoration are essential practices for ensuring data safety and continuity in Linux server management. Ansible, an automation tool, simplifies these tasks by providing a scalable and repeatable solution.

This project will guide us through creating Ansible playbooks to automate the backup and restore process for files on a Linux server.

Objectives
Understand the basics of Ansible and its role in automation.
Set up an Ansible environment for managing Linux servers.
Create a playbook to back up files to a remote or local directory.
Develop a playbook to restore files from a backup.
Test and verify the backup and restore processes.
Prerequisites
Linux Servers: At least one server to act as the target machine and an optional control machine for Ansible.
Ansible Installed: Ansible installed on the control machine. (Refer to the Ansible installation guide to install it if not already installed.)
SSH Access: SSH access between the control machine and target servers with public key authentication.
Tools: A text editor to create and edit Ansible playbooks.
Tasks Outline
Install and configure Ansible on the control machine.
Set up an inventory file for the target Linux server.
Create an Ansible playbook to back up files. Create an Ansible playbook to restore files from a backup.
Test the backup and restore functionality.
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

[linux_servers] target ansible_host=54.221.50.28 ansible_user=ubuntu

AnsibleTarget

Save and close the file.

Task 3 - Create an Ansible Playbook to Back Up Files
Create a playbook file for backup:

nano backup.yml

BackupFile

Add the following playbook content:

BackUpConfiguration

Replace /path/to/files with the path of the files you want to back up.

To get the appropite file path in linux use the command below:

ls "$PWD/file.txt" # or echo "$PWD/file.txt"

BackUpFile

Configfile

Task 4 - Create an Ansible Playbook to Restore Files
Create a playbook file for restoration:

vim restore.yml

RestoreFile

Add the following playbook content:

BackUpRestore

RestoreFile

Replace /path/to/files with the original file location.

Task 5 - Test the Backup and Restore Functionality
Run the backup playbook:

ansible-playbook -i inventory.ini backup.yml

AnsibleBackup

Verify the backup directory and files on the target server:

ls /backup

BackupDir

Run the restore playbook:

ansible-playbook -i inventory.ini restore.yml

Verify the restored files in the original location on the target server:

ls /path/to/files

Conclusion
This project introduced you to automating file backup and restoration on a Linux server using Ansible. You set up an Ansible environment, created playbooks for backup and restoration, and verified the process. With these skills, you can extend the playbooks to include more servers, schedule regular backups, or integrate advanced options like compression or encryption.

END.