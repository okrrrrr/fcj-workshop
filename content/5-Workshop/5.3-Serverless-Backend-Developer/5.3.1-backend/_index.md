---
title : "Preparing Backend Source Code and Creating DynamoDB"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

### Preparing Backend Source Code

First, prepare the system's backend source code. The backend is built using a serverless architecture, where each function is implemented as an AWS Lambda function to handle business logic such as file ingestion, data analysis, status updates, and notification sending.

The source code is organized into **8 Lambda functions**, with each function handling a specific task to ensure the system is easy to manage, scale, and maintain.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image.png)

### Preparing Backend Source

Once the source code is ready, navigate to the previously created backend directory to package and deploy the code to AWS Lambda.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-1.png)

### Packaging Lambda Functions

Next, package all Lambda functions into **.zip** files. Packaging enables AWS Lambda to accept and deploy each function independently.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-2.png)

After running the script, the system automatically generates compressed files for each Lambda function.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-3.png)

Each **.zip** file contains:

- The `app.js` file.
- The `package.json` file.
- The `node_modules` directory.

The packaged files will be used for uploading to the AWS Lambda service in the subsequent steps.

### Creating Amazon DynamoDB

After preparing the backend source code, proceed to create an **Amazon DynamoDB** table to store information and processing status for files uploaded to the system.

In the DynamoDB interface, select **Create table**, enter the table name, and configure the necessary parameters before creating the table.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-4.png)

### Creating a Global Secondary Index

Once the table has been successfully created, navigate to the **Indexes** tab and create a **Global Secondary Index (GSI)** named **userID-index**.

This index is used to search and query data based on **User ID**, helping to improve data retrieval performance during processing and result display.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-5.png)

### Completion

Upon completing the steps above, the system has the backend source code ready, the Lambda functions packaged, and the Amazon DynamoDB database set up, laying the groundwork for deploying the serverless services in the subsequent sections.