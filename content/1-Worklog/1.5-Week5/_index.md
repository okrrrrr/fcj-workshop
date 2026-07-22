---
title: "Week 5 Worklog"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5 Objectives:

* Learn Docker and Container on AWS.
* Learn how to deploy containerized applications with ECS and EKS.
* Practice Infrastructure as Code with CloudFormation and CDK.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed CloudWatch, CloudTrail knowledge from Week 4. Learned Docker basics: images, containers, registries. Understood Dockerfile and how to build images. Learned Docker Compose to manage multi-container applications | 18/05/2026 | 18/05/2026 | <https://docs.docker.com/get-started/introduction/> |
| 3 | Installed Docker Desktop on Windows. Checked docker version. Created simple Dockerfile with nginx image. Built image: docker build -t my-app. Ran container: docker run -d -p 8080:80 my-app. Pushed image to Docker Hub to share with team. Created docker-compose.yml with web app and database services. Ran docker-compose up -d to initialize all containers. Checked running containers with docker ps | 19/05/2026 | 19/05/2026 | <https://000067.awsstudygroup.com/3-containersanddocker/> |
| 4 | Created ECR Repository to store private Docker images. Pushed Docker image to ECR using AWS credentials. Created ECS Cluster with Fargate launch type (serverless container). Created Task Definition with container configuration. Created Service with Load Balancer to distribute traffic. Configured Security Group for container. Checked service running and viewed logs in CloudWatch. Scaled service by increasing desired count to 2 | 20/05/2026 | 20/05/2026 | <https://000016.awsstudygroup.com/> |
| 5 | Created EKS Cluster with eksctl command line tool. Configured kubeconfig: aws eks update-kubeconfig --name my-cluster. Created Node Group with EC2 instances to run pods. Deployed sample app: kubectl apply -f deployment.yaml. Created Service to expose app. Checked pods: kubectl get pods. Scaled deployment: kubectl scale deployment my-app --replicas=3. Installed CDK: npm install -g aws-cdk. Created new project: cdk init app --language python. Wrote Python code to define infrastructure. Deployed S3 bucket: cdk deploy | 21/05/2026 | 21/05/2026 | <https://www.eksworkshop.com/> |
| 6 | Wrote CloudFormation Template (YAML) defining VPC with subnets. Added EC2 Instance and Security Group to template. Added S3 Bucket with bucket policy. Uploaded template to CloudFormation Console. Created Stack and monitored creation progress. Checked Outputs after stack completes to get resource IDs. Created Docker image for web application with multi-stage build. Pushed image to Amazon ECR. Created ECS Cluster with Fargate. Deployed container with ALB integration to route HTTP traffic. Tested application via ALB DNS | 22/05/2026 | 22/05/2026 | <https://000067.awsstudygroup.com/2-prerequiste/2.1-createcloudformation/> |


### Week 5 Achievements:

* Understood and used Docker to build, run and push container images.
* Deployed containerized applications with Amazon ECS Fargate.
* Created Kubernetes cluster with Amazon EKS and deployed applications.
* Written Infrastructure as Code with CloudFormation and CDK.
