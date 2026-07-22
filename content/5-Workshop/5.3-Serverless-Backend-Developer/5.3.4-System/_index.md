---
title : "System Testing"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

### Launching the System

After configuring the AWS services and deploying the entire backend, launch the system to verify the operation of the serverless architecture.

Launch the web application and backend, then access the system's main interface to perform a file upload.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-20.png)

---

### Uploading a File to the System

On the user interface, select a file to test and upload it to Amazon S3.

Immediately after the file is successfully uploaded, Amazon S3 automatically triggers the **S3Handler** Lambda function, which updates the status in Amazon DynamoDB and sends a processing request to Amazon SQS. Next, the **Processor** Lambda function is triggered and launches AWS Step Functions to execute the analysis process.

During processing, the file status is displayed as **Scanning**.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-21.png)

---

### Checking Analysis Results

Once AWS Step Functions completes the entire processing workflow, the system updates the file's final status.

If no malware or anomalies are detected, the result is displayed as **Safe** on the user interface.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-22.png)

---

### Monitoring Data in Amazon DynamoDB

In addition to displaying results on the website, all file information and processing status details are stored in Amazon DynamoDB.

Checking the data in DynamoDB helps verify that synchronization between the backend and the user interface is functioning correctly. Whenever a file's status changes, the corresponding data in DynamoDB is updated and immediately reflected on the website.

---

### Results

Upon completion of testing, the system operates exactly according to the designed workflow:

- The user uploads a file via the web interface.
- Amazon S3 receives the file and triggers the **S3Handler** Lambda function.
- The **S3Handler** Lambda updates the status and sends a request to Amazon SQS.
- Amazon SQS triggers the **Processor** Lambda function to handle the task.
- AWS Step Functions orchestrates the entire analysis process.
- The final results are stored in Amazon DynamoDB.
- The website automatically displays the status and analysis results to the user.

Test results demonstrate successful integration of AWS services, an automated processing workflow, and accurate data synchronization between the backend and the user interface.