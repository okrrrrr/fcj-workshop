---
title : "Preparing the CI/CD Environment"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

### Creating the buildspec.yml file

After completing the Amazon S3 and Lifecycle Rule configuration, the next step is to prepare the **Continuous Integration/Continuous Deployment (CI/CD)** environment. In AWS CodeBuild, the **buildspec.yml** file defines the steps the system executes during the Build and Deploy processes.

Create the **buildspec.yml** file in the project root directory and configure environment variables, the runtime version, and the processing stages.

![](/images/5-Workshop/5.4-Data/image-9.png)

In the **buildspec.yml** file, the build process is divided into key stages:

- **Install:** Install the libraries and environment required for the build process.
- **Pre-build:** Check tool versions and prepare the execution environment.
- **Build:** Compile and package the backend application using AWS SAM.
- **Post-build:** Package and deploy the application to AWS.

### Configuring the Deployment Process

After completing the build steps, proceed to configure the **Post-build** stage in the **buildspec.yml** file.

This stage performs tasks such as:

- Packaging the application using AWS SAM.
- Generating the `packaged.yaml` file.
- Uploading artifacts to Amazon S3.
- Deploying the stack to AWS CloudFormation.
- Storing artifacts for use in subsequent steps of the CI/CD pipeline.

![](/images/5-Workshop/5.4-Data/image-10.png)

### Pushing Source Code to GitHub

Once the **buildspec.yml** file is finalized, save your project changes and synchronize the source code with GitHub.

Commit the changes and use the **git push** command to update the repository from your development machine to GitHub.

![](/images/5-Workshop/5.4-Data/image-11.png)

Storing source code on GitHub enables AWS CodeBuild and AWS CodePipeline to automatically fetch the latest version of the project whenever changes occur, laying the groundwork for the Continuous Integration and Continuous Deployment processes in the subsequent steps.

### Completion

Upon completing the steps above, the CI/CD environment is fully prepared. The project now includes a **buildspec.yml** file defining the build and deployment processes, and the source code has been synchronized to GitHub, ready for integration with AWS CodeBuild and AWS CodePipeline in the following sections.