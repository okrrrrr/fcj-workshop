---
title : "Perimeter Security & Cloud Admin"
date : 2024-01-01
weight : 11
chapter : false
pre : " <b> 5.6. </b> "
---
### Perimeter Security & Cloud Admin

Following the completion of the frontend system, serverless backend, and CI/CD pipeline, the next step involves implementing security and monitoring mechanisms on the Amazon Web Services (AWS) platform. The objective of this phase is to strengthen system protection against unauthorized access, securely manage sensitive information, encrypt data, and monitor all resource activities within the cloud environment.

During the workshop, services such as **AWS Identity and Access Management (IAM)**, **AWS WAF**, **AWS Secrets Manager**, **AWS Key Management Service (KMS)**, **AWS CloudTrail**, and **AWS Config** are utilized to establish a comprehensive security layer. These services facilitate secure authentication between GitHub Actions and AWS, protect API Gateway from attacks, manage encryption keys and secrets, and track and evaluate the configuration state of the entire system.
This section is divided into the following four main topics:

- **5.6.1. Configuring IAM OIDC Provider and GitHub Actions:** Setting up an authentication mechanism between GitHub Actions and AWS using OpenID Connect (OIDC), and creating an IAM role to facilitate the automated deployment process.
- **5.6.2. Configuring AWS WAF to protect API Gateway:** Creating a Web ACL and configuring rules to protect API Gateway against attacks such as DoS or spam requests.
- **5.6.3. Managing encryption keys and secrets:** Using AWS Secrets Manager to store sensitive information and AWS KMS to manage data encryption keys.
- **5.6.4. Monitoring and assessing system compliance:** Configuring AWS CloudTrail and AWS Config to log activities, track resource changes, and assess compliance with security policies.

![Perimeter Security & Cloud Admin](/images/5-Workshop/5.6-Perimeter-Security/image.png)