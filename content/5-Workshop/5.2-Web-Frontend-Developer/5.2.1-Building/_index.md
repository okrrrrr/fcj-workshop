---
title : "Building Frontend React and Amazon Cognito"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

### React Frontend and AWS SDK Directory Structure

First, set up and organize the directory structure for the React frontend application. Organizing folders by function makes the codebase easier to manage, maintain, and scale during development.

The frontend application uses the AWS SDK to connect and interact with AWS services such as Amazon Cognito, Amazon S3, and Cognito Identity Pools.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image.png)

### Creating the AWS.ts File to Configure AWS Services

Within the project directory, create an `AWS.ts` file to store the configuration details required for the connection between the React application and AWS services.

Configuration details typically include:

* AWS Region.
* User Pool ID.
* App Client ID.
* Identity Pool ID.
* S3 Bucket Name.

Managing configuration in a single file simplifies updates and avoids redundant declarations across multiple application components.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-1.png)

### Accessing the AWS Management Console

Access the AWS Management Console and log in using your assigned AWS account to begin configuring the services for the frontend application.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-2.png)

### Searching for the Amazon Cognito Service

In the AWS Management Console interface, enter the keyword `Cognito` into the search bar.

Select the **Amazon Cognito** service from the list of results to access the user authentication management page.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-3.png)

### Create a New User Pool

On the Amazon Cognito management page, select the **Create user pool** function to begin creating a new User Pool.

The User Pool is used to manage user registration, sign-in, and authentication for the React application.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-4.png)

### Configure User Directory

During the User Pool creation process, configure the following settings:

* Select **Single-page application (SPA)** as the application type.
* In the **Name your application** field, enter the application name.
* Select **Email** as the sign-in method.
* Check the **Enable self-registration** box to allow users to register their own accounts.
* Expand the **Select attributes** list.
* Find and select the **Name** attribute.
* Review the configured information.
* Select the function to create the User Pool to complete the process.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-5.png)

### Save the User Pool ID

Once the User Pool has been successfully created, the system redirects to the User Pool overview page.

On the **Overview** page, copy and save the **User Pool ID** value. This information will be used in the `AWS.ts` file to connect the React application to Amazon Cognito.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-6.png)

### Retrieving the App Client ID

In the User Pool management interface, perform the following steps:

*   Select the **Applications** section.
*   Select **App clients**.
*   Locate the App Client that was created alongside the User Pool.
*   Copy and save the **Client ID** value.
*   Click on the App Client name to view its details.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-7.png)

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-8.png)

### Editing the App Client

On the App Client details page, select **Edit** to review or update settings relevant to the React application.

Once finished, save the changes and update the **User Pool ID** and **Client ID** values ​​in the `AWS.ts` file.