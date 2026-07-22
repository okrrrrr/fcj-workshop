---
title: "Week 4 Worklog"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4 Objectives:

* Learn Monitoring and Logging services: CloudWatch, CloudTrail.
* Learn how to use AWS Config for compliance management.
* Practice setting up monitoring system for applications.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Auto Scaling, Load Balancer knowledge from Week 3. Learned about CloudWatch: metrics, alarms, dashboards, logs. Learned CloudWatch Logs Insights for complex log queries. Understood metric filters and subscription filters | 11/05/2026 | 11/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Accessed CloudWatch Console. Created new Dashboard with widgets displaying CPU, Memory, Network metrics. Created Alarm for CPU Utilization > 80%. Created Alarm for Disk Space < 20%. Configured SNS Topic with email subscription to receive notifications when alarm triggers. Installed CloudWatch Agent on EC2 to collect custom metrics. Configured logs from Apache view in CloudWatch Logs | 12/05/2026 | 12/05/2026 | <https://000008.awsstudygroup.com/vi/> |
| 4 | Accessed CloudTrail Console. Created new Trail configure to send logs to separate S3 Bucket. Enabled CloudWatch Logs integration for log analysis. Created bucket policy for CloudTrail access. Performed AWS operations (create EC2, S3) to generate events. Checked Event History to see all API calls made. Downloaded and analyzed log file from S3 to understand JSON log structure | 13/05/2026 | 13/05/2026 | <https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-getting-started.html> |
| 5 | Accessed AWS Config Console. Enabled AWS Config and selected S3 bucket to store configuration history. Selected IAM Role for AWS Config. Viewed Resource inventory to see list of all resources in account. Created custom Config Rule (e.g., require encrypted S3 buckets). Viewed compliance status of EC2 instances. Created CloudWatch Event rule to automatically respond when non-compliance occurs. Accessed Systems Manager Console. Created Document to run commands on EC2. Used Run Command to install software on multiple instances at once instead of SSH into each machine | 14/05/2026 | 14/05/2026 | <https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html> |
| 6 | Created VPC with Public and Private Subnets. Launched EC2 instances with Auto Scaling Group. Configured CloudWatch Dashboard to monitor all metrics in one central location. Set up CloudWatch Alarms for all important services. Enabled CloudTrail to log all API calls for audit purposes. Enabled AWS Config to track resource changes and compliance. Created SNS Topic with subscription to receive alerts when issues occur. Created CloudWatch Composite Alarm combining multiple metrics. Tested by creating high load verify alarms trigger correctly. Checked CloudTrail logs to verify complete audit trail | 15/05/2026 | 15/05/2026 | <https://000008.awsstudygroup.com/vi/> |


### Week 4 Achievements:

* Created and configured CloudWatch Dashboard to monitor application metrics.
* Set up CloudWatch Alarms and SNS notifications for alerts.
* Enabled and used CloudTrail to audit API calls.
* Configured AWS Config to track resource compliance.
* Used Systems Manager to manage EC2 instances efficiently.
