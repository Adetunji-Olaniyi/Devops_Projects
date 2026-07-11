# Mini Project: Configuring Auto Scaling with ALB using Launch Template

Purpose:
In this mini project, we will learn how to configure Auto Scaling in AWS with an Application Load Balancer (ALB) using a Launch Template. The project aims to demonstrate the automatic scaling of EC2 instances based on demand, while leveraging the benefits of a Launch Template.

Objectives:
Create Launch Template:

Learn how to create a Launch Template with the required specifications.
Set Up Auto Scaling Group:

Configure an Auto Scaling group to manage the desired number of EC2 instances using the Launch Template.
Configure Scaling Policies:

Set up scaling policies to adjust the number of instances based on demand.
Attach ALB to Auto Scaling Group:

Connect the Auto Scaling group to an existing ALB.
Test Auto Scaling:

Verify that the Auto Scaling group adjusts the number of instances in response to changes in demand.
Project Tasks:
Task 1: Create Launch Template**
1. Log in to the AWS Management Console.

![](./img/01.AWSConsole.png)


2. Navigate to the EC2 service.

![](./img/02.Instances.png)

3. In the left navigation pane, click on "Launch Templates."
![](./img/03.%20launchtemplate.png)

4. Click the "Create launch template" button.

![](./img/04.LaunchTemplate.png)

5. Configure the launch template settings, including the AMI, instance type, and user data
![](./img/05.%20Template1.png)
![](./img/06.%20Template2.png)
![](./img/07.%20Template3.png)
![](./img/08.%20Template4%20UserData.png)
![](./img/09.%20TemplateCreated.png)

Task 2: Set Up Auto Scaling Group
1. In the AWS Management Console, navigate to the EC2 service.

![](./img/10.%20ec2.png)

2. In the left navigation pane, click on "Auto Scaling Groups.
![](./img/11.%20AutoScalinggroup.png)

3. Click the "Create Auto Scaling group" button.

![](./img/12.%20ASG.png)

4. Choose "Use Launch Template" and select the Launch Template you created.
![](./img/13.%20ChooseASG.png)

5. Configure the Auto Scaling group settings, including the group name, desired capacity, and initial instances.

![](./img/14.%20ASG1.png)
![](./img/15.ASG2.png)
![](./img/16.%20Capacity.png)

6. Set up additional configurations such as network settings, subnets, and scaling policies.
![](./img/17.%20Settings.png)
![](./img/17.ASG3.png)
![](./img/18.%20ASG.png)
![](./img/19.ASG2.png)
![](./img/20.%20ASG.png)

Task 3: Configure Scaling Policies
1. In the Auto Scaling group configuration, navigate to the "Scaling policies" section.

![](./img/21.%20AutoScaling%20(1).png)

2. Click on "Create scaling policy" and configure policies for scaling in and scaling out based on demand.
![](./img/22.ScalingInandOut.png)

Task 4: Attach ALB to Auto Scaling Group
1. In the Auto Scaling group configuration, navigate to the "Load balancing" section.

![](./img/23.%20ALB.png)
![](./img/24.ALB.png)
![](./img/25.%20ALB2.png)
![](./img/26.ALB3.png)
![](./img/27.ALB.png)
![](./img/28.MyALB.png)

2. Click on "Edit" and select the ALB to associate with the Auto Scaling group.
![](./img/29.EditASG.png)
![](./img/30.%20AttcaheALB.png)
![](./img/31.Attached.png)
![](./img/32.SaveandUpdate.png)

Task 5: Test Auto Scaling
1. Generate traffic to trigger scaling policies.
![](./img/33.Traffic.png)
![](./img/34.%20InstanceCreatedwithASG.png)

2. Connect to Instance using EC2 Instance Connect
![](./img/35.Connected.png)

2. Monitor the Auto Scaling group and verify that the number of instances adjusts based on demand.

END.