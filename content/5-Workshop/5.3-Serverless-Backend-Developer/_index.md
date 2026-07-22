---
title : "Building a Serverless Backend"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Building a Serverless Backend

In this section, we will build a **Serverless Backend** system on the Amazon Web Services (AWS) platform to handle the entire analysis workflow for files uploaded from the frontend application. The serverless architecture is implemented by combining various AWS services—such as **AWS Lambda**, **Amazon DynamoDB**, **Amazon SQS**, **AWS Step Functions**, and **Identity and Access Management (IAM)**—to create an automated, server-management-free processing pipeline.

The system's workflow begins when a user uploads a file to Amazon S3. An S3 event automatically triggers Lambda functions to receive the request, update the processing status, send information to an Amazon SQS queue, and orchestrate the analysis process via AWS Step Functions. Throughout the process, the status of each file is stored in Amazon DynamoDB and synchronized with the user interface. Once the analysis is complete, the system returns the results for the user to view directly on the website.

The workshop content is divided into key sections: preparing the backend source code, configuring AWS services, building the processing workflow using Step Functions, and testing the entire system.

To facilitate implementation and monitoring, the **Building a Serverless Backend** section is divided into the following four main parts:

- **5.3.1. Preparing Backend Source Code and Creating Amazon DynamoDB:** Prepare the backend source code, package AWS Lambda functions, and create an Amazon DynamoDB database to store processing data.
- **5.3.2. Configuring Amazon SQS and AWS Lambda:** Create an Amazon SQS queue, configure IAM roles, deploy Lambda functions, and set up triggers linking Amazon S3, Amazon SQS, and AWS Lambda.
- **5.3.3. Building AWS Step Functions:** Create a State Machine, configure IAM roles, and build a workflow to orchestrate Lambda functions for the automated analysis process.
- **5.3.4. System Testing:** Launch the system, upload files via the website, monitor processing status, and verify results in Amazon DynamoDB and the user interface.

![Serverless Backend](/images/5-Workshop/5.3-Serverless-Backend-Developer/image.png)