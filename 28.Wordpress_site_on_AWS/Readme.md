
# Capstone Project: WordPress Site on AWS

## Project Scenario

A small to medium-sized digital marketing agency, **"DigitalBoost"**, wants to enhance its online presence by creating a high-performance **WordPress-based** website for their clients. The agency needs a scalable, secure, and cost-effective solution that can handle increasing traffic and seamlessly integrate with their existing infrastructure. Your task as an AWS Solutions Architect is to design and implement a WordPress solution using various AWS services, such as Networking, Compute, Object Storage, and Databases.

---

## Pre-requisite

* Knowledge of TechOps Essentials

---

The project overview with necessary architecture have been provided as you help **DigitalBoost** with her Wordpress-Based Website. Kindly follow the instructions below to complete this Capstone Project. Also, necessary scripts have been provided **here**.

---

# Project Deliverables

### Documentation:

* Detailed documentation for each component setup.
* Explanation of security measures implemented.

### Demonstration:

* Live demonstration of the WordPress site.
* Showcase auto-scaling by simulating increased traffic.

---

# Project Overview

*(Architecture diagram shown in image.)*

### Architecture Notes

1. VPC with public and private subnets in 2 availability zones.
2. An Internet Gateway is used to allow communication between instances in VPC and the Internet.
3. We are using 2 Availability Zones for high availability and fault tolerance.
4. Resources such as NAT Gateway, Bastion Host, and Application Load Balancer use Public Subnets.
5. We will put the webservers and database servers in the Private Subnets to protect them.
6. The NAT Gateway allows the instances in the private App subnets and private Data subnets to access the internet.
7. We are using an MYSQL RDS database.
8. We are using Amazon EFS so that the webservers can have access to shared files.
9. The EFS Mount Targets are in each AZ in the VPC.
10. We are using EC2 Instances to host our website.
11. Application Load Balancer is used to distribute web traffic across an Auto Scaling Group of EC2 instances in multiple AZs.
12. Using Auto Scaling Group to dynamically create our EC2 instances to make our website highly available, scalable, fault-tolerant, and elastic.
13. We are using Route 53 to register our Domain name and create a record set.

---

# Project Components

# 1. VPC Setup

## VPC ARCHITECTURE

*(Architecture diagram shown in image.)*

### Objective

Create a Virtual Private Cloud (VPC) to isolate and secure the WordPress infrastructure.

### Steps

* Define IP address range for the VPC.
* Create VPC with public and private subnets.
* Configure route tables for each subnet.

---

# 2. Public and Private Subnet with NAT Gateway

## NAT GATEWAY ARCHITECTURE

*(Architecture diagram shown in image.)*

### Objective

Implement a secure network architecture with public and private subnets. Use a NAT Gateway for private subnet internet access.

### Steps

* Set up public subnet for resources accessible from the internet.
* Create private subnet for resources with no direct internet access.
* Configure a NAT Gateway for private subnet internet access.

---

# 3. AWS MySQL RDS Setup

## SECURITY GROUP ARCHITECTURE

*(Architecture diagram shown in image.)*

### Objective

Deploy a managed MySQL database using Amazon RDS for WordPress data storage.

### Steps

* Create an Amazon RDS instance with MySQL engine.
* Configure security groups for RDS instance.
* Connect WordPress to the RDS database.

---

# 4. EFS Setup for WordPress Files

### Objective

Utilize Amazon Elastic File System (EFS) to store WordPress files for scalable and shared access.

### Steps

* Create an EFS file system.
* Mount the EFS file system on WordPress instances.
* Configure WordPress to use the shared file system.

---

# 5. Application Load Balancer

### Objective

Set up an Application Load Balancer to distribute incoming traffic among multiple instances, ensuring high availability and fault tolerance.

### Steps

* Create an Application Load Balancer.
* Configure listener rules for routing traffic to instances.
* Integrate Load Balancer with Auto Scaling group.

---

# 6. Auto Scaling Group

### Objective

Implement Auto Scaling to automatically adjust the number of instances based on traffic load.

### Steps

* Create an Auto Scaling group.
* Define scaling policies based on metrics like CPU utilization.
* Configure launch configurations for instances.



## Project Scenario

You are acting as an **AWS Solutions Architect** for a digital marketing agency called **DigitalBoost**.

The goal is to deploy a **highly available, scalable, secure, and cost-effective WordPress website** using AWS.

---

# Architecture Components

The completed architecture contains:

```
Internet
      │
Route53
      │
Internet Gateway
      │
Application Load Balancer
      │
Auto Scaling Group
      │
─────────────────────────────────────
Availability Zone A      Availability Zone B

EC2 WordPress            EC2 WordPress
      │                       │
──────────── Amazon EFS ────────────
              │
         Amazon RDS MySQL
```

---

# AWS Services Used

| Service              | Purpose                               |
| -------------------- | ------------------------------------- |
| VPC                  | Isolated network                      |
| Public Subnets       | ALB, NAT Gateway                      |
| Private App Subnets  | WordPress EC2                         |
| Private Data Subnets | MySQL RDS                             |
| Internet Gateway     | Internet Access                       |
| NAT Gateway          | Internet access for private instances |
| EC2                  | WordPress server                      |
| RDS                  | MySQL Database                        |
| EFS                  | Shared WordPress files                |
| ALB                  | Load balancing                        |
| Auto Scaling         | High Availability                     |
| Route53              | DNS                                   |

---

# Deliverables

You must provide

* Documentation
* Screenshots
* Live WordPress site
* Auto Scaling demonstration

---

# Project Breakdown

## Part 1 — VPC Setup

Objective

Create a secure Virtual Private Cloud.

Tasks

* Create a VPC

```
CIDR

10.0.0.0/16
```

Create

* Internet Gateway

Attach it to the VPC.

Create

### Public Subnets

```
AZ1
10.0.0.0/24

AZ2
10.0.1.0/24
```

Create

### Private App Subnets

```
AZ1
10.0.2.0/24

AZ2
10.0.3.0/24
```

Create

### Private Database Subnets

```
AZ1
10.0.4.0/24

AZ2
10.0.5.0/24
```

---

## Part 2 — Route Tables

Create

Public Route Table

Route

```
0.0.0.0/0

Internet Gateway
```

Associate

* Public Subnet AZ1
* Public Subnet AZ2

Create

Private Route Table

Associate

* Private App AZ1
* Private App AZ2
* Private DB AZ1
* Private DB AZ2

---

## Part 3 — NAT Gateway

Create

Elastic IP

↓

Create

NAT Gateway

↓

Place NAT Gateway inside Public Subnet

↓

Edit Private Route Table

Destination

```
0.0.0.0/0
```

Target

```
NAT Gateway
```

---

## Part 4 — Security Groups

Create

### ALB Security Group

Allow

```
HTTP 80

HTTPS 443

Source

0.0.0.0/0
```

---

### SSH Security Group

Allow

```
22

Source

Your IP
```

---

### Web Server Security Group

Allow

```
80

443

Source

ALB SG
```

Allow

```
22

Source

SSH SG
```

---

### Database Security Group

Allow

```
3306

Source

Web Server SG
```

---

### EFS Security Group

Allow

```
2049

Source

Web Server SG
```

---

# Part 5 — Amazon RDS

Create

```
MySQL
```

Deploy

* Multi-AZ

Place

Database Subnet Group

using

Private Database Subnets.

Attach

Database Security Group

Save

```
Database Endpoint

Username

Password
```

You'll use these later.

---

# Part 6 — Amazon EFS

Create

Elastic File System

Attach

Mount Targets

inside

Both Private Subnets

Attach

EFS Security Group

---

# Part 7 — EC2 WordPress

Launch

Amazon Linux

(or Ubuntu if instructed)

Place inside

Private App Subnets

Attach

* Web Server SG
* SSH SG

Install

```
Apache

PHP

MySQL client

Amazon EFS utilities
```

Mount

Amazon EFS

to

```
/var/www/html
```

Download

WordPress

Configure

```
wp-config.php
```

Use

Database Endpoint

---

# Part 8 — Application Load Balancer

Create

Internet-facing

Application Load Balancer

Place inside

Public Subnets

Attach

ALB Security Group

Create

Target Group

Register

WordPress EC2

---

# Part 9 — Auto Scaling

Create

Launch Template

↓

Use WordPress EC2

↓

Create

Auto Scaling Group

↓

Attach

Application Load Balancer

↓

Desired Capacity

```
2
```

Minimum

```
2
```

Maximum

```
4
```

Scaling Policy

CPU > 70%

---

# Part 10 — Route53

Register

Domain

or use an existing one.

Create

Hosted Zone

Create

A Record

Alias

↓

Application Load Balancer

---

# Final Testing

Open

```
http://your-domain.com
```

Complete WordPress installation.

---

# Screenshots Required

Take screenshots of:

* VPC
* Subnets
* Route Tables
* NAT Gateway
* Security Groups
* RDS
* EFS
* EC2
* Load Balancer
* Auto Scaling Group
* Route53
* WordPress Home Page
* WordPress Admin Dashboard
