---
title : "Configuring AWS WAF to Protect API Gateway"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

### Creating a Web ACL

After completing the configuration of the IAM OIDC Provider and GitHub Actions, the next step is to deploy **AWS Web Application Firewall (AWS WAF)** to enhance system protection against internet-based attacks.

Navigate to the **AWS WAF & Shield** service and select **Create web ACL** to initialize a new **Web Access Control List (Web ACL)**. This Web ACL will be used to control and filter requests sent to **Amazon API Gateway**.

![](/fcj-workshop/images/5-Workshop/5.6-Perimeter-Security-&-Cloud-Admin/image-5.png)

### Completing Web ACL Creation

After configuring the necessary details—such as the name, Region, and the resource to be protected—proceed to create the Web ACL.

![](/fcj-workshop/images/5-Workshop/5.6-Perimeter-Security-&-Cloud-Admin/image-6.png)

Once successfully created, the Web ACL will be associated with the API Gateway to inspect and evaluate all incoming requests before they are forwarded to the backend.

### Configuring a Rate-based Rule

Next, create a **Rate-based Rule** to limit the number of requests an IP address can send to the API Gateway within a specific timeframe.

![](/fcj-workshop/images/5-Workshop/5.6-Perimeter-Security-&-Cloud-Admin/image-7.png)

In this configuration, set the action to **Block** for IP addresses that send more than **100 requests within 5 minutes**. This rule helps restrict requests sent at abnormally high frequencies, thereby mitigating the risk of Denial of Service (DoS) attacks or API spam.

### The Role of AWS WAF

Once configured, AWS WAF performs the following functions:

- Inspects requests sent to Amazon API Gateway.
- Automatically blocks IP addresses that exceed the configured access threshold.
- Mitigates the risk of DoS attacks and API spam.
- Protects the system against anomalous traffic.
- Strengthens application-layer security before requests are forwarded to the backend.

### Completion

Upon completing the steps above, the system has successfully deployed **AWS WAF** to protect Amazon API Gateway. The Web ACL, combined with a **Rate-based Rule**, helps monitor traffic, automatically blocks requests that exceed permitted limits, and enhances the overall security of the system.