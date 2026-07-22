---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---
### Overview

This workshop involves building an automated cloud-based platform for malware analysis and detection on **Amazon Web Services (AWS)** using a serverless architecture. The system allows users to upload files for inspection via a web interface, subsequently automating the analysis and processing workflow and returning results within the cloud environment.

To construct the complete system, various AWS services are integrated to handle specific functions. The user interface is developed using React, with authentication managed by Amazon Cognito. Files are stored on Amazon S3, and the entire processing workflow is executed using AWS Lambda in conjunction with Amazon SQS, Amazon DynamoDB, and AWS Step Functions, adhering to a serverless architecture.

Additionally, the system implements **Continuous Integration and Continuous Deployment (CI/CD)** pipelines using AWS CodeBuild and AWS CodePipeline to automate application build and deployment processes. Security mechanisms—including IAM, AWS WAF, AWS Secrets Manager, AWS KMS, AWS CloudTrail, and AWS Config—are also configured to enhance system protection, manage access rights, secure sensitive information, and monitor all AWS resource activities.

Finally, the **Amazon VPC Endpoint** solution was implemented to establish a private connection between Amazon Virtual Private Cloud (Amazon VPC) and Amazon S3, enabling system resources to access AWS services via the internal network—bypassing the public Internet—thereby enhancing the security and performance of the entire platform.


### Contents

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Web Frontend Developer](5.2-Web-Frontend-Developer/)
3. [Serverless Backend Developer](5.3-Serverless-Backend-Developer/)
4. [Data](5.4-Data/)
5. [AI Security Analyst & Web Admin](5.5-AI-Security-Analyst-%26-Web-Admin/)
6. [Perimeter Security & Cloud Admin](5.6-Perimeter%20Security%20%26%20Cloud%20Admin/)