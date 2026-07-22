---
title : "Prerequiste"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.5.1. </b> "
---

### Preparing Network Infrastructure

#### Create VPC

![alt text](image.png)

#### Create public and private subnets

![alt text](image-1.png)

#### Create Internet Gateways

![alt text](image-2.png)

#### Create NAT Gateway

![alt text](image-3.png)

#### Create Route Table

![alt text](image-4.png)

### Preparing EC2 Instances

#### Create two EC2 instances:

Bastion Host (Public Subnet)

![alt text](image-5.png)

AI Server (Private Subnet)

![alt text](image-6.png)

### Preparing Security Groups

Configure Security Groups for the EC2 instances.

Bastion Host (Public Subnet)

![alt text](image-8.png)

AI Server (Private Subnet)

![alt text](image-7.png)

### Preparing IAM Role

Create IAM Role

![alt text](image-9.png)