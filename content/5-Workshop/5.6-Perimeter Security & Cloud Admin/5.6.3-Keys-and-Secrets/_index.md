---
title : "Managing Encryption Keys and Secrets"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

### Creating a Secret in AWS Secrets Manager

After configuring AWS WAF, the next step is to deploy **AWS Secrets Manager** to centrally manage the system's sensitive information.

Access the **AWS Secrets Manager** service, select **Store a new secret**, and proceed to create a new Secret.

![](/images/5-Workshop/5.6-Perimeter-Security/image-8.png)

Store critical information within the Secret, such as:

- API Keys.
- Database passwords.
- Other authentication credentials used during system deployment and operation.

Using AWS Secrets Manager allows applications to securely access sensitive information without needing to store it directly in source code or configuration files.

### Creating a Customer Managed Key with AWS KMS

After creating the Secret, proceed to configure **AWS Key Management Service (AWS KMS)** to manage the encryption keys used to protect system data.

Create a **Customer Managed Key (CMK)** named **kms-project-key**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-9.png)

This encryption key is used to:

- Encrypt data stored on AWS services.
- Protect Secrets stored in AWS Secrets Manager.
- Support other AWS services requiring data encryption or decryption.
- Ensure that only authorized resources and users can use the encryption key.

### Roles of Secrets Manager and AWS KMS

Combining AWS Secrets Manager and AWS KMS offers numerous benefits for system security, including:

- Centralized management of sensitive information.
- Reduced risk of exposing API keys or passwords within source code.
- Data encryption using organization-managed keys.
- Support for access control via IAM policies.
- Compliance with security and data management requirements in cloud environments.

### Completion

Upon completing the steps above, the system is successfully configured with **AWS Secrets Manager** for storing secrets and **AWS KMS** for managing encryption keys. Integrating these two services enhances data protection, minimizes the risk of information leakage, and strengthens the overall security posture of the system.