---
title : "Monitoring and Evaluating System Compliance"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

### Configuring AWS CloudTrail

After configuring security mechanisms, the next step is to deploy **AWS CloudTrail** to log all activities occurring within the AWS account.

Access the **AWS CloudTrail** service, select **Create trail**, and proceed to create a new trail named **main-project-trail**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-10.png)

CloudTrail automatically records administrative actions, configuration changes, and events occurring across AWS services. All audit logs are stored in Amazon S3 to facilitate monitoring, auditing, and analysis as needed.

### Configuring AWS Config

Next, deploy **AWS Config** to continuously monitor the configuration state of system resources.

In the AWS Config interface, configure the **Configuration Recorder** to capture all configuration changes across AWS services.

![](/images/5-Workshop/5.6-Perimeter-Security/image-11.png)

Once the Configuration Recorder is activated, AWS Config automatically tracks resource changes and evaluates compliance levels based on established rules.

### Checking Compliance Rules

After completing the configuration, check the evaluation results for the rules in AWS Config.

In the system, the **s3-bucket-public-read-prohibited** rule is used to verify that public access to Amazon S3 buckets is prevented.

![](/images/5-Workshop/5.6-Perimeter-Security/image-12.png)

The result shows a **Compliant** status, indicating that the S3 buckets meet security requirements and do not allow unauthorized public read access.

### Monitoring the AWS Config Dashboard

Finally, access the **AWS Config Dashboard** to view an overview of the compliance status for all resources in the system.

![](/images/5-Workshop/5.6-Perimeter-Security/image-13.png)

The dashboard provides information such as:

- The number of resources being monitored by AWS Config.
- Compliance evaluation results for each rule.
- Compliance status of Amazon S3 buckets.
- Statistics on resources that meet or do not meet security requirements.
- An overview report that enables administrators to easily monitor the system.

### Completion

Upon completing the steps above, the system has successfully deployed **AWS CloudTrail** and **AWS Config** to monitor activity and evaluate the compliance status of AWS resources. CloudTrail captures comprehensive administrative logs, while AWS Config continuously tracks configuration states and checks for compliance with security policies. This allows administrators to quickly detect changes, review activity history, and maintain a secure, stable cloud environment.