---
title : "Configuring AWS Lambda"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5.5 </b> "
---

### Introduction

- In this section, you will create and configure an AWS Lambda function to handle URL analysis requests from Amazon API Gateway. The Lambda function acts as an intermediary between API Gateway and the Bastion Host; it forwards requests to the Nginx reverse proxy running on the Bastion Host and receives analysis results from the Flask API on the private EC2 instance before returning the final result to the user.

### Creating the Lambda Function

+ Lambda configuration:
    + Function name: url-analyzer-lambda
    + Runtime: Node.js 22.x
    + Architecture: x86_64
    + Execution role: Create a new role with basic Lambda permissions

![alt text](image.png)

### Configuring Environment Variables

- Select **Configuration → Environment variables → Edit.**

![alt text](image-1.png)

### Updating Lambda Source Code

- After updating the source code, select **Deploy**.

![alt text](image-2.png)

- The Lambda function has been successfully deployed.

### Testing the Lambda Function

- Select **Test** and create a test event:

```
{
  "body": "{\"url\":\"https://google.com\"}"
}
```

![alt text](image-3.png)

- The Lambda function test was successful, correctly identifying whether the URL is safe or malicious.