---
title : "Configuring S3, Identity Pool, and IAM Role"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2.2. </b> "
-------------------------

### Creating an Amazon S3 Bucket

Navigate to the **Amazon S3** service in the AWS Management Console.

On the S3 management page, select **Create bucket** to start creating a new bucket for storing application files.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-9.png)

### Configuring S3 Bucket Details

On the bucket creation page, perform the following steps:

* Enter a name in the **Bucket name** field.
* Select the AWS Region appropriate for your system.
* Keep the default settings or adjust them as required.
* Scroll to the bottom of the page.
* Select **Create bucket** to finish.

The bucket name must be globally unique across the entire Amazon S3 system.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-10.png)


### Configuring CORS for the S3 Bucket

After successfully creating the bucket, select the newly created bucket and perform the following steps:

* Select the **Permissions** tab.
* Scroll down to the **Cross-origin resource sharing (CORS)** section.
* Select **Edit**.
* Enter the CORS configuration to allow the React application to access the S3 bucket.
* Select **Save changes** to save the configuration.

Configuring CORS enables the browser to allow the frontend application to send requests to Amazon S3 from a different domain or port.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-11.png)


### Creating a Cognito Identity Pool

Return to the Amazon Cognito service and navigate to the **Identity pools** management section.

Select the option to create a new Identity Pool to grant users access to AWS resources after they log in.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-12.png)


### Configuring Access Permissions for the Identity Pool

During the Identity Pool configuration step, perform the following actions:

* Select **Authenticated access**.
* Choose **Amazon Cognito user pool** as the authentication source.
* Click **Next** to proceed.
* Select the **User Pool ID** created in the previous section.
* Select the corresponding **App Client ID**.
* Leave the other settings as-is unless changes are required.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-13.png)


### Configuring the IAM Role for the Identity Pool

After linking the User Pool and App Client, click **Next** to move to the access permission configuration step.

At this stage, AWS will either create an IAM Role or allow you to select one for authenticated users.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-14.png)


### Naming the Identity Pool

In the **Identity pool name** field, enter a name for the Identity Pool.

Then:

* Review the configured information.
* Click **Next** to proceed.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-15.png)


### Reviewing and Creating the Identity Pool

On the confirmation page, review the following details:

* Identity Pool name.
* Access type.
* User Pool ID.
* App Client ID.
* Associated IAM Role.

If the information is correct, proceed to create the Identity Pool.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-16.png)


Once successfully created, copy and save the **Identity Pool ID** value to update the `AWS.ts` file.

### Accessing Amazon IAM

Navigate to the **Identity and Access Management (IAM)** service in the AWS Management Console.

In the IAM interface, select **Roles** to view the list of existing roles.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-17.png)


### Selecting the Identity Pool IAM Role

Locate the IAM role created by AWS for authenticated users of the Cognito Identity Pool.

The role name typically includes the Identity Pool name and a phrase indicating authenticated users.

Select the role to view and configure its permissions.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-18.png)


![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-19.png)


### Adding Amazon S3 Access Permissions

On the IAM role details page, perform the following steps:

* Select the **Permissions** tab.
* Select **Add permissions**.
* Select **Attach policies**.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-20.png)


### Attaching the AmazonS3FullAccess Policy

In the policy search box, enter:

```text
AmazonS3FullAccess
```

Then proceed to:

* Check the box for the **AmazonS3FullAccess** policy.
* Select **Attach policies** to assign the permission to the IAM role.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-21.png)


### Verifying the Configuration

Once completed, review the configuration details in the `AWS.ts` file, including:

* AWS Region.
* User Pool ID.
* App Client ID.
* Identity Pool ID.
* S3 Bucket name.

Next, run the React application and verify the following capabilities:

* Account registration.
* User login.
* Authentication via Amazon Cognito.
* Obtaining access permissions from the Identity Pool.
* Connecting to and interacting with Amazon S3. The test results confirm that the frontend application is correctly connected to the AWS services.