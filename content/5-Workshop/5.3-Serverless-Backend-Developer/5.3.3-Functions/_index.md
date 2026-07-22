---
title : "Building AWS Step Functions"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

### Creating an IAM Role for AWS Step Functions

After configuring Amazon SQS and the AWS Lambda functions, the next step is to create an **IAM Role** for **AWS Step Functions**. This IAM Role grants the necessary permissions for Step Functions to invoke Lambda functions and access Amazon DynamoDB while orchestrating the workflow.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-16.png)

The IAM Role is granted necessary permissions such as:

- Executing AWS Lambda functions.
- Reading and writing data to Amazon DynamoDB.
- Writing activity logs to Amazon CloudWatch Logs.

Once created, the IAM Role will be assigned to the State Machine in AWS Step Functions.

---

### Creating AWS Step Functions

Next, navigate to the **AWS Step Functions** service and create a new **State Machine** to orchestrate the entire file processing workflow.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-17.png)

After creating the State Machine, configure the states and link them to their corresponding Lambda functions.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-18.png)

The system workflow consists of the following key steps:

- **Validate:** Check the information and status of the uploaded file.
- **Analyze:** Perform analysis and inspection of the file.
- **Notify:** Update the final result and notify the user.

Each step in the workflow invokes a separate Lambda function, ensuring the processing logic is decoupled, easy to manage, and scalable.

---

### Updating ARNs for Lambda Functions

Once the State Machine has been successfully created, copy its **ARN (Amazon Resource Name)** and update the environment variables for the following Lambda functions:

- `malware-analysis-update-dev`
- `malware-analysis-s3-handler-dev`
- `malware-analysis-processor-dev`

Configuring the ARN enables these Lambda functions to trigger the State Machine whenever a new processing request arises.

---

### Verifying the Workflow

After completing the configuration, verify the entire workflow within AWS Step Functions to ensure that states are correctly linked and execute in the proper sequence.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-19.png)

The workflow operates in the following sequence:

1. The user uploads a file to Amazon S3.
2. Amazon S3 triggers the **S3Handler** Lambda function.
3. The **S3Handler** Lambda updates the status and sends a message to Amazon SQS.
4. Amazon SQS triggers the **Processor** Lambda function.
5. The **Processor** Lambda initiates the AWS Step Functions workflow.
6. AWS Step Functions executes the steps in order: **Validate → Analyze → Notify**.
7. The final result is updated in Amazon DynamoDB for display on the user interface.

### Completion

Upon completing the steps above, the system has successfully established an orchestration process using **AWS Step Functions**. The entire processing workflow is automated, enabling Lambda functions to coordinate in the correct sequence, reducing inter-component dependencies, and enhancing system scalability.