---
title : "Database & CI/CD Engineer"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### Database & CI/CD Engineer

After completing the development of the Frontend and Serverless Backend, the next step is to implement the data storage system and establish an automated application deployment pipeline (CI/CD). In this section, the system utilizes Amazon S3 to store uploaded files while configuring Lifecycle Rules to optimize storage costs and manage the data lifecycle.

Additionally, the Continuous Integration and Continuous Deployment (CI/CD) process is built using AWS services such as CodeBuild and CodePipeline. This pipeline automates the compilation, testing, and deployment of the application whenever source code is updated on GitHub, thereby minimizing manual intervention and ensuring a rapid, accurate, and consistent development process.

The content of this section is divided into four main parts:

- **5.4.1. Configuring Amazon S3 and Lifecycle Rules:** Creating a data storage bucket and configuring Lifecycle Rules to manage file lifecycles.
- **5.4.2. Preparing the CI/CD Environment:** Creating the `buildspec.yml` file, configuring the build process, and pushing source code to GitHub.
- **5.4.3. Setting up AWS CodeBuild:** Creating a CodeBuild project and configuring the build environment to automate application compilation.
- **5.4.4. Setting up AWS CodePipeline:** Creating a pipeline, connecting GitHub to CodeBuild, and configuring the automated application deployment process.

![Data & CI/CD](/images/5-Workshop/5.4-Data/image.png)