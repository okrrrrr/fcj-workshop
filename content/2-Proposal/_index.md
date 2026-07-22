---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# Serverless AI Malware Sandbox & Analysis Platform  
## An Isolated AWS Serverless Environment for Automatic AI-Driven Malware Behavior Analysis  


### 1. Executive Summary  
The **Serverless AI Malware Sandbox & Analysis Platform** is designed to build a secure, automated, and cost-efficient malware analysis environment on AWS for cybersecurity engineers and software developers. The platform enables users to register and log in securely, upload suspect files directly to S3 via API Gateway and Lambda Presigned URLs. An event-driven asynchronous workflow queues upload requests via Amazon SQS and coordinates analysis using AWS Step Functions, launching a suspect file into a completely isolated VPC Sandbox network (no Internet access) to execute AI behavioral analysis models on an EC2 instance. Scan histories and results are stored in DynamoDB and presented on a web dashboard hosted via AWS Amplify. The platform implements rigorous security baselines, including AWS WAF protecting the API Gateway, AWS KMS encryption for all storage, AWS Secrets Manager for secret storage, and AWS Config with EventBridge for automatic configuration error correction (Auto-remediation).


### 2. Problem Statement  
*The Problem*  
Analyzing suspect malware files usually requires setting up expensive local hardware laboratories or using public sandboxes, which carry significant risks of leaking sensitive proprietary data. Additionally, manual analysis is time-consuming, difficult to automate when large volumes of files are uploaded simultaneously without queuing mechanisms, and analytical nodes can easily crash under high load. Furthermore, maintaining analysis virtual machines 24/7 on the cloud leads to substantial budget waste for smaller teams or research groups.  


*The Solution*  
The platform addresses these issues through a combined architecture of AWS Serverless, isolated VPC Sandbox network, and automatic AI-driven classification models:  
- **Authentication & Secure Upload**: Amazon Cognito manages user access. Amazon S3 allows clients to upload files directly via Presigned URLs to prevent network bottlenecks at the processing layers.  
- **Serverless Backend & Queuing**: AWS Lambda and API Gateway process request routing efficiently. Amazon SQS queue combined with Step Functions coordinates analysis jobs to prevent server overload.  
- **Isolated VPC Sandbox for AI Models**: Amazon VPC implements Private Subnets with no Internet route, accessing S3, DynamoDB, and CloudWatch internally via VPC Endpoints. An EC2 instance runs the machine learning model to classify behavior and record logs via CloudWatch.  
- **Database & DevOps (Automation)**: Amazon DynamoDB stores scanning history. CI/CD pipelines automate deployment using AWS CodePipeline & CodeBuild. An S3 Lifecycle rule automatically deletes suspect files after 7 days to manage storage and ensure safety.  
- **Perimeter Security & Audit**: AWS WAF blocks spam API calls, AWS KMS encrypts all data at rest, AWS Secrets Manager manages passwords, and AWS Config coupled with EventBridge automatically locks S3 buckets within 1 second if they are accidentally made public.  


*Benefits and Return on Investment (ROI)*  
The solution delivers automated testing that reduces analysis time from hours to minutes under absolute sandbox safety. Operations costs are dramatically optimized thanks to an intelligent scheduling mechanism (turning on the EC2 analysis node only when files are queued for scanning), reducing monthly infrastructure cost from **$51.40/month** (24/7 run) to only **$5.20/month** (development/test run). Break-even is expected in 3–6 months due to decreased manual processing hours and reduced commercial analysis tool license fees.  


### 3. Solution Architecture  
The platform employs a serverless event-driven architecture to ensure complete isolation and high throughput. Web client data is authenticated by Cognito, requests a Presigned URL from Lambda via API Gateway, and uploads directly to a raw S3 bucket. A new file event triggers SQS queuing and Step Functions coordination to spin up the isolated EC2 node in the VPC Sandbox (no Internet Gateway) to analyze the file securely via VPC Gateway Endpoints, logging results into DynamoDB.  

![Architecture Diagram](/images/2-Proposal/architecture-diagram.png)  


*AWS Services Used*  
- **Amazon Cognito**: Manages user registration, login, and access sessions.  
- **Amazon S3**: Stores raw uploads and implements Lifecycle rules for auto-deletion after 7 days.  
- **Amazon API Gateway & AWS Lambda**: Provides the API gateway and executes Python logic for generating URLs/fetching scan logs.  
- **Amazon SQS & Step Functions**: Queues analysis requests and coordinates state machine workflows.  
- **Amazon DynamoDB**: Stores user scan history and behavioral analysis results.  
- **Amazon VPC**: Designs a completely isolated sandbox network with no Internet access (Private Subnets, VPC Endpoints).  
- **Amazon EC2 (or ECS)**: Runs machine learning models in the isolated sandbox.  
- **AWS CodePipeline & CodeBuild**: Automates the CI/CD pipeline from GitHub to AWS.  
- **AWS Amplify**: Connects to the Hugo Git repository to automatically host the report site.  
- **AWS WAF**: Web Application Firewall protecting API Gateway with rate limits against spam IP requests.  
- **AWS Secrets Manager & KMS**: Secures API credentials/passwords and encrypts all stored data.  
- **AWS Config & EventBridge**: Monitors cloud security configurations and automatically resolves compliance errors.  
- **Amazon CloudWatch & CloudTrail**: Collects AI process logs and keeps system audit records.  


*Component Design*  
- **Client & Edge Access**: Web frontend calls API Gateway, authenticates with Cognito, and uploads files to S3 via Presigned URL.  
- **API Backend**: API Gateway forwards requests to Lambda. Lambda runs business logic and pushes new file events to SQS.  
- **Queuing & Coordination**: SQS stores events, and Step Functions manages EC2 instances, ensuring the AI node runs only when files are waiting and stops when idle.  
- **Isolated Sandbox**: VPC Sandbox prevents analyzed malware from connecting to hacker command-and-control (C2) servers.  
- **Auto Cleanup**: S3 Lifecycle rule runs daily to wipe malicious files older than 7 days.  


### 4. Technical Implementation  
*Implementation Phases*  
The project is divided into 4 major phases:  
1. **Research & Architectural Design (Late April)**: Investigate sandbox analysis methods, design the isolated VPC network, and model the asynchronous workflow.  
2. **Infrastructure & CI/CD Setup (May)**: Construct core resources (VPC, S3, DynamoDB, Cognito) on AWS and configure automatic CI/CD using CodePipeline.  
3. **AI Module & Backend Development (June)**: Install AI models on the EC2 Sandbox, write Lambda functions for queue ingestion, and integrate Cognito authentication into the frontend.  
4. **Security Hardening & Testing (July)**: Set up WAF rules, KMS encryption keys, configure AWS Config Auto-remediation, execute system load tests, and hand over the system.  


*Technical Requirements*  
- **Sandbox Environment**: Strict VPC with no Internet Route, utilizing Interface/Gateway VPC Endpoints for S3, DynamoDB, and CloudWatch to handle internal communication securely.  
- **AI Engine**: EC2 instance (t3.medium configuration) configured with malware analysis tools and machine learning models for file classification.  
- **Backend & CI/CD**: Python code for Lambda using the AWS SDK (Boto3). Configure buildspec files for CodeBuild to automatically build and deploy new pushes.  


### 5. Timeline & Milestones  
- **Pre-Internship (Before April 20)**: Outline project goals, research sandbox theories, and diagram cloud architecture.  
- **During Internship (April 20 – July 25)**:  
    - **Late April**: Learn AWS infrastructure and set up the isolated VPC Sandbox.  
    - **May**: Deploy API Gateway, Lambda, SQS, DynamoDB, and integrate Cognito authentication.  
    - **June**: Implement the AI classification engine in EC2, and complete the web frontend.  
    - **July**: Execute comprehensive security testing, optimize infrastructure costs, and hand over for production by July 25.  
- **Post-Launch (After July 25)**: Maintain operations and investigate feature upgrades for up to 1 year.  


### 6. Budget Estimation  
Detailed infrastructure costs calculated using the [AWS Pricing Calculator](https://calculator.aws/):  


*Infrastructure Costs (Optimized for Testing)*  
- **Amazon EC2 (t3.medium)**: Machine learning VM in Sandbox. Cost 24/7: ~$33.00/month. Optimized cost (only active for tests): **~$2.50/month**.  
- **AWS WAF**: Firewall protecting API Gateway. Cost 24/7: ~$7.00/month. Optimized cost (only active for tests): **~$0.50/month**.  
- **VPC Endpoints**: Internal connection gateways. Cost 24/7: ~$9.00/month. Optimized cost (only active for tests): **~$0.60/month**.  
- **AWS KMS**: Data encryption key. Cost: **~$1.00/month**.  
- **AWS Secrets Manager**: Vault for passwords/secrets. Cost: **~$0.40/month**.  
- **AWS Config**: Automated configuration audit. Cost 24/7: ~$1.00/month. Optimized cost: **~$0.20/month**.  
- **Other Serverless Services (S3, Lambda, API Gateway, SQS, DynamoDB, Amplify)**: Fully covered by the **AWS Free Tier** during development/testing.  


*Total Estimated Cost*:  
- **24/7 Operation**: ~$51.40/month  
- **Optimized Testing Operation (Active during tests only)**: **~$5.20/month**  


### 7. Risk Assessment  
*Risk Matrix*  
- **Malware Escapes to Internet**: High impact, low probability (due to isolated VPC Sandbox design).  
- **Cost Overrun (Forgotten EC2)**: Medium impact, medium probability (if left running continuously).  
- **Spam Upload Attack**: Medium impact, medium probability.  


*Mitigation Strategies  
- **Network Isolation**: Strip Internet Gateways from the VPC Sandbox, and restrict Security Groups to internal traffic only.  
- **Cost Control**: Deploy automation scripts to stop the EC2 VM after 30 minutes of inactivity, and configure AWS Budgets alerts to trigger at $5.00.  
- **Spam Prevention**: Apply AWS WAF rate limiting to block spam IPs and enforce strict S3 upload size limits (e.g., maximum 10MB per file).  


*Contingency Plans*  
- Maintain AWS CloudFormation/CDK configurations to quickly reconstruct the infrastructure layout if any critical configuration failure occurs.  


### 8. Expected Outcomes  
*Technical Improvements*: Successfully build a fully automated, secure, and isolated malware analysis sandbox on AWS.  
*Long-term Value*: Provide a safe file scanning tool for the lab group, accumulating advanced DevSecOps and cloud security architecture experience on AWS.

