---
title: "Week 3 Worklog"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives:

* Learn Auto Scaling and Elastic Load Balancing (ELB).
* Learn how to use DynamoDB - AWS NoSQL database.
* Practice deploying applications with Load Balancer and Auto Scaling.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed VPC, Security Group knowledge from Week 1-2. Learned about Auto Scaling: why we need automatic instance scaling. Learned about ELB: difference between Application LB vs Network LB vs Gateway LB | 04/05/2026 | 04/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Created Launch Template with EC2 (Amazon Linux 2 AMI). Configured User Data to auto-install Apache. Created Target Group for Load Balancer. Created Application Load Balancer (ALB) with Security Group open port 80/443. Initialized Auto Scaling Group with min=1, max=3 instances. Configured Scaling Policy based on CPU Utilization target 70%. Tested Auto Scaling with load test | 05/05/2026 | 05/05/2026 | <https://000006.awsstudygroup.com/> |
| 4 | Accessed DynamoDB Console. Created new Table with Partition Key (user_id). Selected Capacity Mode (On-Demand or Provisioned). Added items to table (user_id, name, email). Created Global Secondary Index (GSI) to query by email. Enabled Point-in-time Recovery (PITR). Created On-Demand Backup for table. Connected DynamoDB from Lambda function | 06/05/2026 | 06/05/2026 | <https://000060.awsstudygroup.com/> |
| 5 | Created RDS Instance with MySQL (t2.micro). Enabled Multi-AZ Deployment for high availability. Enabled Encryption for RDS Instance. Created Read Replica to distribute read operations. Connected RDS from EC2 using MySQL Client. Created custom Parameter Group (max_connections). Created Option Group to enable BACKUP. Created Secret to store RDS username/password in Secrets Manager. Configured Lambda to read secret from Secrets Manager instead of hardcoding credentials | 07/05/2026 | 07/05/2026 | <https://000005.awsstudygroup.com/> |
| 6 | Designed VPC with 2 Availability Zones (ap-southeast-1a, ap-southeast-1b). Created Public Subnet in each AZ for ALB and Private Subnet for EC2. Created NAT Gateway in Public Subnet so Private subnet has internet access. Launched EC2 instances in Auto Scaling Group. Configured Application Load Balancer to distribute traffic across 2 AZs. Created RDS with Multi-AZ in Private Subnet ensuring database is always available. Deployed web application to EC2. Tested failover by terminating one instance and verified website still works via ALB DNS | 08/05/2026 | 08/05/2026 | <https://000101.awsstudygroup.com/> |


### Week 3 Achievements:

* Successfully understood and deployed Auto Scaling Group with Load Balancer.
* Created and managed DynamoDB Table, used GSI and backup.
* Deployed Web Application with High Availability (Multi-AZ).
* Configured RDS Multi-AZ and Read Replica.
* Used Secrets Manager to manage credentials securely.
