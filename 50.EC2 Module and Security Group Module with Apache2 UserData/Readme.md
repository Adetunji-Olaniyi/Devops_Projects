EC2 Module and Security Group Module with Apache2 UserData
Mini Project: EC2 Module and Security Group Module with Apache2 UserData
Purpose:
In this mini project, we will use Terraform to create modularized configurations for deploying an EC2 instance with a specified Security Group and Apache2 installed using UserData.

Objectives:
Terraform Module Creation:

Learn how to create Terraform modules for modular infrastructure provisioning.
EC2 Instance Configuration:

Configure Terraform to create an EC2 instance.
Security Group Configuration:

Create a separate module for the Security Group associated with the EC2 instance.
UserData Script:

Utilize UserData to install and configure Apache2 on the EC2 instance.
Project Tasks:
Task 1: EC2 Module
Create a new directory for your Terraform project (e.g., terraform-ec2-apache).

Inside the project directory, create a directory for the EC2 module (e.g., modules/ec2).

Write a Terraform module (modules/ec2/main.tf) to create an EC2 instance.

Task 2: Security Group Module
Inside the project directory, create a directory for the Security Group module (e.g., modules/security_group).

Write a Terraform module (modules/security_group/main.tf) to create a Security Group for the EC2 instance.

Task 3: UserData Script
Write a UserData script to install and configure Apache2 on the EC2 instance. Save it as a separate file (e.g., apache_userdata.sh).

Ensure that the UserData script is executable (chmod +x apache_userdata.sh).

Task 4: Main Terraform Configuration
Create the main Terraform configuration file (main.tf) in the project directory.

Use the EC2 and Security Group modules to create the necessary infrastructure for the EC2 instance.

Task 5: Deployment
Run terraform init terraform valdiate terraform plan and terraform apply to deploy the EC2 instance with Apache2.

Access the EC2 instance and verify that Apache2 is installed and running.

Install and configure the following:
AWS Account

AWSAccount

AWS CLI aws --version

AWSVersion

Configure AWS credentials aws configure

awsconfig

Fill in: Access Key, Secret Key, Region (e.g. us-east-1).

Terraform terraform --version

Terraform

Project Structure
We’ll create a tidy Terraform project with two modules:

ProjectStructure

Instructions:
Create a new directory for your Terraform project using a terminal (mkdir terraform-ec2-apache).

mkdirapache

Change into the project directory (cd terraform-ec2-apache).

cdtoapached

Create directories for the EC2 and Security Group modules (mkdir -p modules/ec2 and mkdir -p modules/security_group).

mkdir -p modules/ec2

ec2dir

mkdir -p modules/security_group

sgdir

Write the EC2 module configuration (vi modules/ec2/main.tf) to create an EC2 instance.

EC2 Module

modules/ec2/variables.tf

vim modules/ec2/variables.tf

variablefile variableconfigfile

modules/ec2/main.tf

vim modules/ec2/main.tf

mainfile mainconfigfile

modules/ec2/outputs.tf

vim modules/ec2/outputs.tf

outputmodule outputconfig

Write the Security Group module configuration (nano modules/security_group/main.tf) to create a Security Group.

Security Group Module

modules/security_group/variables.tf

modules/security_group/variables.tf

sgvaraiablefile sgvariavleconfig

modules/security_group/main.tf

modules/security_group/main.tf

sgmainfile sgmainconfig sgmainconfig

modules/security_group/outputs.tf

modules/security_group/outputs.tf

sgoutputfile sgoutputconfig

Write the UserData script (nano apache_userdata.sh) to install and configure Apache2.

UserData Script (Apache install)

Create apache_userdata.sh:

userdatafile userdataconfig

If you later switch to an Ubuntu AMI, change yum to apt, httpd to apache2, and service name to apache2.

Make the UserData script executable (chmod +x apache_userdata.sh).

Make it executable:

chmod +x apache_userdata.sh

userdataexe

Create the main Terraform configuration file (nano main.tf) and use the EC2 and Security Group modules.

Root Configuration

providers.tf (Provider + Backend optional)

touch provider.tf

providerfile proc=viderconf

variables.tf

variabletffile variabletfconfig

outputs.tf (Root outputs)

outputfile outputcong

main.tf (Wire modules together)

mainfile mainconf

Run terraform init and terraform apply to deploy the EC2 instance with Apache2.

terraform init

TFInit

terraform validate

TFValidate

terraform plan

TFPlan TFPlan

terraform apply

TFapply TFApply

Access the EC2 instance using its public IP and verify that Apache2 is installed and running.

AWSPage

Accessing the page using Public IP

34.245.31.115

WebPage

Document your observations and any challenges faced during the project.

Troubleshooting & Tips
No public IP / Site not reachable

Ensure instance is in a public subnet with an Internet Gateway. We set associate_public_ip_address = true. If your VPC/subnet overrides this, supply a known public subnet via -var="public_subnet_id=subnet-xxxx". Check SG allows TCP/80 from 0.0.0.0/0.

UserData didn’t run

Check /var/log/cloud-init-output.log and /var/log/cloud-init.log. Ensure script is attached via user_data = file("apache_userdata.sh"). If you changed to Ubuntu, ensure you updated package manager (apt) and service name (apache2).

AMI not found

The AMI filter is for Amazon Linux 2 x86_64. For arm64 or Ubuntu, change the data "aws_ami" filter. Region-specific AMIs differ; the most_recent filter helps.

SSH timeout

Ensure your allowed_ssh_cidr includes your IP. Verify the instance got a public IP and routing to IGW is correct.

Clean Up

terraform destroy

TFDestroy TFDestroy

Side Note:
Ensure you have the AWS CLI installed and configured with appropriate credentials.
Modify variables and configurations in the modules based on your specific requirements.
This is a learning exercise; use it to gain hands-on experience with Terraform, EC2, UserData, and Security Groups.
END.