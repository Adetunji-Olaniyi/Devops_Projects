# Mini Project - Terraform EC2 Instance and AMI Creation
In this mini project, we will use Terraform to automate the creation of an EC2 instance on AWS and then create an Amazon Machine Image (AMI) from that instance.

Objectives
Learn how to write basic Terraform configuration files.
Learn how to write Terraform script to automate creation of an EC2 instance on AWS.
Learn how to use Terraform script to automate the creation of an AMI from an already created EC2 instance on AWS.

Prerequisites
This project requires you to have an AWS Account and the AWS CLI configured to it locally. This setup will be used by the Terraform script you are going to write. From your local command line interface, Terraform will use the configured AWS CLI credential to communicate with your AWS Account when executing the script.

Ensure you have an AWS Account created and functional. You may see a guide here to create a new AWS account.https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-creating.html

Ensure you have the AWS CLI installed and configured with the credentials of your AWS Account. You may see a guide here. https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
Ensure you have Terraform installed on your computer. You may see a guide
Tasks Outline
Confirm the Prerequisites
Write the Script
Execute the Script
Initialize [init]
Validate [validate]
Plan [plan]
Apply [apply]
Confirm Resources
Clean up
Destroy [destroy]

Project Tasks
Task 1 - Confirm the Prerequisites
Login into your AWS Account to confirm it is functional.

![](./img/01.%20Login%20console.png)


Run aws --version on your terminal to confirm the AWS CLI is installed. You should see an output similar to this.
![](./img/02.%20awscli.png)

Run aws configure list to confirm the AWS CLI is configured. You should see an output similar to this.
![](./img/03.%20AWSConfiglist.png)


Run aws sts get-caller-identity to verify that the AWS CLI can successfully authenticate to your AWS Account. You should see an output similar to this.
AWSidentity

Run terraform --version to confirm Terraform is installed. You should see an output similar to this.
![](./img/05.%20TerraformVersion.png)

Task 2 - Developing the Terraform Script to create EC2 Instance and AMI from it
Create a new directory for this Terraform project: mkdir terraform-ec2-ami and cd 

Inside this directory, create a Terraform configuration file: vim main.tf.

![](./img/06.%20MakeDirectory.png)
![](./img/07.%20cdtoterraform.png)

Inside this file, write the script to create an EC2 instance specifying instance type, ami, and tags. Extend this script to include the creation of an AMI from the created EC2 Instance. (See sample below)
Script

Formalized Script
Script

Script Explanation
This script creates an EC2 instance and then creates an AMI from that instance.

Provider Block:

provider "aws" tells Terraform to use AWS as the cloud provider
region = "us-east-1" specifies which AWS region to use
EC2 Instance Creation

resource "aws_instance" "my_ec2_spec" creates an EC2 Instance
ami = ami-0ecb62995f68bb549" specifies the Amazon Machine Image ID to use for the instance
instance_type = "t2.micro" defines the EC2 Instance type
The tag block adds a name tag to the instance for identification
AMI Creation from the EC2 Instance

resource "aws_ami" "my_ec2_spec_ami" creates an AMI from the EC2 Instance
name = "my-ec2-ami" names the new AMI
source_instance_id = aws_instance.my_ec2_spec.id uses the EC2 Instance to create the AMI
Task 3 - Executing the Terraform Script
Initialize the Terraform project using terraform init

Terraforminit

Validate the correctness of this script using terraform validate

Terraform Validate

Confirm the resources that will be created by the execution of this script using terraform plan

Terraform Plan

Apply the Terraform configuration using terraform apply

Terraform Apply

TfApply

Task 4 - Confirm Resources
Confirm the creation of the EC2 Instance and its AMI in your AWS Account according to the specified details.

ConfirmCreationinAWSDashboard

Task 5 - Clean up
Execute command terraform destroy to clean up the resources created by the script.

TFDestry

TFDestry

END.