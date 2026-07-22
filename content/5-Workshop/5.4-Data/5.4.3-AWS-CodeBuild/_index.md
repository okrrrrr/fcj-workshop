---
title : "Setting up AWS CodeBuild"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

### Creating an AWS CodeBuild Project

Once the source code has been pushed to GitHub and the **buildspec.yml** file configuration is complete, the next step is to create a project in **AWS CodeBuild** to automatically compile and package the application.

Navigate to the **AWS CodeBuild** service, select **Create build project**, and enter basic information such as the Project name, Source Provider, and the GitHub repository to be used.

![](/images/5-Workshop/5.4-Data/image-12.png)

### Configuring the Build Environment

Next, configure the execution environment for AWS CodeBuild. In this section, select the **Amazon Linux** operating system, the runtime appropriate for the application, and an AWS-provided image.

Additionally, select the **On-demand** mode so that CodeBuild automatically initializes the environment when a build request is made, helping to optimize usage costs.

![](/images/5-Workshop/5.4-Data/image-13.png)

The key parameters to configure include:

- **Provisioning model:** On-demand.
- **Environment image:** Managed image.
- **Compute:** EC2.
- **Running mode:** Container.
- **Operating System:** Amazon Linux.
- **Runtime:** Standard.
- **Image:** AWS CodeBuild Managed Image.

After completing the environment configuration, AWS CodeBuild will use these parameters to create the build environment whenever the pipeline is triggered.

### Launching the CodeBuild Project

After completing the configuration, create the project and verify the operational status of AWS CodeBuild.

![](/images/5-Workshop/5.4-Data/image-14.png)

On the project interface, users can monitor information such as:

- Status of the most recent build.
- Linked repository.
- Build artifact storage location.
- Build process logs.
- Build execution history.

Monitoring this information helps quickly detect errors and evaluate build results before proceeding to the automated deployment step using AWS CodePipeline.

### Completion

Upon completing the steps above, the **AWS CodeBuild** project has been successfully created and configured. The system is now ready to automatically fetch source code from GitHub, execute the build process according to the **buildspec.yml** file, and generate artifacts for deployment via AWS CodePipeline.