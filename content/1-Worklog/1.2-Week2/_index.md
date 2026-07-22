---
title: "Week 2 Worklog"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Review IAM, EC2 from Week 1 and master foundational knowledge.
* Learn important services: Lambda (Serverless), S3, RDS, CloudWatch.
* Practice deploying complete web application on AWS.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed IAM from Week 1: Users, Groups, Roles, Policies. Learned about Lambda - how Serverless model differs from EC2. When to use Lambda vs EC2. Understood how Lambda handles requests, cold start, pricing | 27/04/2026 | 27/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Created EC2 Instance (t2.micro, Amazon Linux 2). Configured Security Group open port 22 (SSH) and port 80 (HTTP). Connected via SSH using Git Bash. Installed and configured Apache web server, enabled auto-start service. Created and mounted EBS volume for data storage | 28/04/2026 | 28/04/2026 | <https://000004.awsstudygroup.com/> |
| 4 | Created S3 Bucket with globally unique name. Uploaded objects (text files, images). Enabled Versioning to track file change history. Created Lifecycle rule to automatically move data to Glacier after 30 days. Configured Static Website Hosting for static site. Created Bucket Policy for public read access | 29/04/2026 | 29/04/2026 | <https://000057.awsstudygroup.com/> |
| 5 | Created DB Subnet Group with at least 2 subnets in different Availability Zones. Created Security Group for RDS open port 3306 (MySQL). Initialized RDS Instance with MySQL engine (t2.micro), saved endpoint and credentials for connection. Connected from EC2 using MySQL Client. Created database, table and inserted data for testing. Accessed CloudWatch Dashboard to view metrics. Created Alarm to monitor CPU usage > 80%. Created SNS Topic and subscription to receive email notifications when alarm triggers | 30/04/2026 | 30/04/2026 | <https://000005.awsstudygroup.com/> |
| 6 | Created first Lambda Function with Python runtime. Wrote simple request handler code. Configured API Gateway as trigger to call Lambda via HTTP. Tested function and viewed logs in CloudWatch. Practiced configuring Environment Variables and set Memory/Timeout. Designed VPC with Public Subnet (contains EC2) and Private Subnet (contains RDS). Launched EC2 in Public Subnet and configured Internet Gateway. Launched RDS in Private Subnet for database security. Configured NAT Gateway so EC2 can download packages. Deployed web application to EC2 and connected to RDS | 01/05/2026 | 01/05/2026 | <https://000101.awsstudygroup.com/> |


### Week 2 Achievements:

* Mastered IAM, EC2, S3 knowledge through hands-on labs.
* Understood key differences between Serverless (Lambda) and Traditional (EC2).
* Successfully created RDS Instance and connected from EC2.
* Deployed first Lambda Function with API Gateway trigger.
* Built complete Web Application with VPC, EC2 and RDS.
