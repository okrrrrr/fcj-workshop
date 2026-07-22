---
title: "Week 1 Worklog"
date: 2026-04-20
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Objectives:

* Complete procedures to receive AWS Credits from FCAJ.
* Understand Cloud Computing overview and AWS infrastructure (Region, AZ, Edge Location).
* Learn basic knowledge about VPC, Subnet, Route Table, Internet Gateway, NAT Gateway.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Meet FCAJ team members, introduce yourself to get familiar, receive AWS account information and credits guide from mentor, read and note internship unit rules and regulations, create personal 12-week internship plan with specific milestones | 20/04/2026 | 20/04/2026 | <https://app.notion.com/p/Group-description-TP-HCM-347df829a730809a8f63d39505644917> |
| 3 | Understand what AWS is and why use Cloud (scalability, flexibility, cost-efficiency), learn about Region, Availability Zone, Edge Location to understand global infrastructure, learn AWS service types: Compute (EC2, Lambda), Storage (S3), Networking (VPC), Database (RDS), Security (IAM), Management (CloudWatch) | 21/04/2026 | 21/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | Create AWS Free Tier Account: Go to aws.amazon.com, click "Create an AWS Account", enter email, password, select "Personal" account, enter personal info and credit card for identity verification, verify phone number via call or SMS, confirm email from AWS, select Support Plan (Basic) to complete registration. Install AWS CLI: Download AWS CLI v2 for Windows from aws.amazon.com/cli, run installer and follow instructions, open Command Prompt check version: aws --version, go to IAM Console → Users → create Access Key for programmatic access, run aws configure enter Access Key ID, Secret Access Key, region (ap-southeast-1), verify credentials using aws sts get-caller-identity | 22/04/2026 | 22/04/2026 | <https://000011.awsstudygroup.com/> |
| 5 | IAM Lab: Go to IAM Console, create first IAM User with programmatic access, attach Policy directly to user (e.g., AmazonEC2ReadOnlyAccess), create Group "Developers" to group users with same responsibilities, assign policy to group instead of attaching directly to user, add user to group to inherit permissions, create Role for EC2 with AmazonS3ReadOnlyAccess policy so EC2 can read S3. EC2 Lab: Learn Instance Types: t2 (general purpose), m5 (compute optimized), c5 (memory optimized), select appropriate AMI: Amazon Linux 2, Ubuntu, or Windows, create Key Pair in EC2 Console and download .pem file for SSH, configure Instance Details including VPC, Subnet, Security Group, Review and Launch Instance, connect via SSH using PuTTY (Windows) or Git Bash (Mac/Linux) | 23/04/2026 | 23/04/2026 | <https://000002.awsstudygroup.com/> |
| 6 | VPC Lab: Create new VPC with CIDR block 10.0.0.0/16 to define IP range for network, create Public Subnet with CIDR 10.0.1.0/24 in first Availability Zone, create Private Subnet with CIDR 10.0.2.0/24 to host private resources, create Internet Gateway (IGW) and attach to VPC to enable internet access, create Route Table for public subnet, add route: Destination 0.0.0.0/0 → Target IGW to allow outbound traffic, associate public subnet with the route table. Security Group & NACL Lab: Create Security Group for EC2 with default deny policy, add Inbound Rule: SSH (port 22) for maintenance, HTTP (port 80) and HTTPS (port 443) for web traffic, create Network ACL with rule numbering (100, 200...) to control traffic at subnet level, associate NACL with subnet and understand difference between SG (stateful) and NACL (stateless) | 24/04/2026 | 24/04/2026 | <https://000003.awsstudygroup.com/> |


### Week 1 Achievements:

* Completed AWS Credits procedures, AWS account is active.
* Successfully installed and configured AWS CLI on local machine.
* Learned basic knowledge about IAM, EC2, EBS, VPC, S3.
* Successfully created first VPC with Public and Private Subnet.
* Configured Internet Gateway and Route Table.
