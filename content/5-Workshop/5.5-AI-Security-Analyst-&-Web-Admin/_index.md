---
title : "System configuration and integration"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

#### VPC endpoints

+ In this workshop, a system is built to simulate the deployment of a real-world application on Amazon Web Services (AWS). The system utilizes an architecture combining AWS services with an artificial intelligence (AI) model to analyze and detect URLs exhibiting signs of phishing.

+ The application follows a multi-tier model: the user interface is built using React; analysis requests are processed via Amazon API Gateway and AWS Lambda, then forwarded to an AI server running Flask on Amazon EC2 to generate predictions and return results to the user. This architecture facilitates scalability, enhances security, and reduces the load on processing components.

#### Overview

+ Designing the AWS network infrastructure, including VPC, Public Subnet, Private Subnet, Internet Gateway, NAT Gateway, and Route Table.

+ Deploying a Bastion Host and EC2 instances within a Private Subnet to ensure a secure network configuration.

+ Configuring Security Groups and IAM Roles for AWS resources.

+ Deploying an AI application using Flask on EC2 to analyze URLs.

+ Configuring an Nginx Reverse Proxy to forward requests from the Bastion Host to the AI ​​server.

+ Setting up AWS Lambda and API Gateway to connect the frontend with the AI ​​system.

![alt text](image.png)



