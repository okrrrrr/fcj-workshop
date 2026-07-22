---
title : "Configuring IAM OIDC Provider and GitHub Actions"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

### Creating an IAM OIDC Provider for GitHub Actions

After completing the CI/CD workflow setup, the next step is to establish a secure authentication mechanism between **GitHub Actions** and **AWS** using **OpenID Connect (OIDC)**. This method allows GitHub Actions to access AWS resources using temporary credentials, eliminating the need to store **AWS Access Keys** and **Secret Access Keys** in the source code.

Navigate to the **AWS Identity and Access Management (IAM)** service, select **Identity Providers**, and create a new **OIDC Provider** for GitHub Actions.

![](/images/5-Workshop/5.6-Perimeter-Security/image.png)

### Verifying the OIDC Provider

Once created, check the **Identity Providers** list to confirm that AWS has linked with the address **token.actions.githubusercontent.com**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-1.png)

Using OIDC enables GitHub Actions to authenticate directly with AWS via an Access Token issued during workflow execution, thereby enhancing system security.

### Creating an IAM Role for GitHub Actions

Next, create a new **IAM Role** and select **Web Identity** as the **Trusted Entity**. This IAM Role will grant GitHub Actions temporary access to the AWS account following successful authentication via OIDC.

![](/images/5-Workshop/5.6-Perimeter-Security/image-2.png)

During the role creation process, assign the **AdministratorAccess** permission to ensure GitHub Actions has the necessary privileges to deploy AWS resources within the CI/CD pipeline. ![](/images/5-Workshop/5.6-Perimeter-Security/image-3.png)

### Finalizing the IAM Role Configuration

Once configuration is complete, the **GitHubActions-Deploy** IAM Role will appear in the **IAM Roles** list and be ready for use in GitHub Actions workflows.

![](/images/5-Workshop/5.6-Perimeter-Security/image-4.png)

This IAM Role will be referenced in the GitHub Actions workflow configuration file to automate tasks such as building, deploying, and managing AWS resources, eliminating the need for static access keys.

### Completion

Upon completing the steps above, an authentication mechanism between GitHub Actions and AWS using **OpenID Connect (OIDC)** has been successfully established. This solution enhances security, minimizes the risk of AWS access key exposure, and supports automated application deployment within the cloud environment.