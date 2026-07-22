---
title : "Configuring Amazon SQS and AWS Lambda"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

### Creating Amazon SQS

After preparing the backend source code and the DynamoDB database, the next step is to create an **Amazon Simple Queue Service (Amazon SQS)** instance. This service acts as an intermediary queue that stores processing requests, ensuring system stability even when multiple users upload files simultaneously.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-6.png)

Once the queue is successfully created, copy the **Queue URL** and save it for use when configuring the Lambda functions.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-7.png)

Proceed to name the queue and complete the creation process.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-8.png)

The system utilizes two types of queues:

- **Main Queue**: Holds processing requests sent from Amazon S3 after users upload files.
- **Dead Letter Queue (DLQ)**: Stores requests that have failed after multiple processing attempts, facilitating easier monitoring and troubleshooting.

Using SQS enables asynchronous communication between system components, enhancing scalability and reducing the load on processing services.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-9.png)

### Creating an IAM Role for AWS Lambda

To enable Lambda functions to access AWS services such as Amazon S3, DynamoDB, Amazon SQS, and Step Functions, you need to create an **IAM Role** and grant it the necessary permissions.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-10.png)

Once the IAM Role is created, proceed to create the **AWS Lambda functions** and upload the **.zip** files prepared in the previous step to their respective functions.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-11.png)

### Configuring the Amazon S3 Trigger

Next, configure an **Amazon S3 Event Notification** so that whenever a user uploads a file to the bucket, Amazon S3 automatically triggers the **S3Handler** Lambda function.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-12.png)

The **S3Handler** Lambda function performs the following tasks:

- Receives information about the file just uploaded to Amazon S3.
- Updates the file's status in Amazon DynamoDB to **received**.
- Sends a message to Amazon SQS for further processing.

### Configuring the Amazon SQS Trigger

After the message is sent to the Amazon SQS queue, configure a trigger so that each new message automatically invokes the **Processor** Lambda function.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-13.png)

The **Processor** Lambda function performs the following tasks:

- Reads the message from Amazon SQS.
- Updates the file's status in DynamoDB to **scanning**.
- Initiates the processing workflow via AWS Step Functions. ![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-14.png)

After completing the trigger configuration, review all Lambda functions to ensure the triggers have been correctly linked.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-15.png)

### Updating the environment configuration file

Finally, update the **.env** file with details such as the Queue URL, DynamoDB table name, S3 bucket name, and necessary ARNs to ensure the Lambda functions can correctly communicate with AWS services.

### Completion

Once the steps above are completed, Amazon SQS and AWS Lambda will be successfully configured. From this point on, whenever a user uploads a file to Amazon S3, the system will automatically receive the request, update the processing status, and proceed to orchestrate the workflow using AWS Step Functions.