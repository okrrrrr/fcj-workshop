---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# VPC ENDPOINTS — THE KEY TO BUILDING AN ISOLATED SANDBOX ON AWS


## How it started...


When our team began building the malware analysis system on AWS, the very first requirement from our mentor was crystal clear: **"The VM running the AI analysis model must be in a completely isolated network — no Internet access whatsoever."**


Sounds simple enough — just remove the Internet Gateway from the VPC, right? But reality hit different. Once we removed the Internet Gateway, our EC2 instance inside the Sandbox lost connectivity to **every** external AWS service — including S3 (where suspect files are stored), DynamoDB (where scan results go), and CloudWatch Logs (where we track AI progress). The AI model ran successfully but... total silence. Nothing was written anywhere.


That's when we discovered **VPC Endpoints** — the solution that lets resources inside a VPC communicate with AWS services without going through the Internet.


## What is a VPC Endpoint?


In simple terms, a VPC Endpoint is like a **private tunnel** that connects directly from your VPC to a specific AWS service, traveling entirely through AWS's internal backbone network (AWS PrivateLink). Traffic never leaves Amazon's infrastructure.


There are **2 types** of VPC Endpoints:


### 1. Gateway Endpoint (Free 💰)
- Supports **S3** and **DynamoDB** only
- Works by adding a route entry to your subnet's Route Table
- **Zero cost** — this is crucial for budget optimization
- Simple setup: create the endpoint, select route tables, done


### 2. Interface Endpoint (Charged per hour + data)
- Supports **most other AWS services** (CloudWatch Logs, SQS, EC2 API, SSM, KMS...)
- Works by creating an **Elastic Network Interface (ENI)** in your subnet with a private IP
- Costs approximately **~$0.01/hour/AZ** + data transfer fees
- Requires **Private DNS** enabled so SDKs/CLI automatically resolve to the correct endpoint


## Our Sandbox Architecture


![VPC Endpoint Architecture](/fcj-workshop/images/3-Blog/blog1_vpc_endpoint.png)


As shown above, here's the Sandbox network architecture our team designed:


- **Sandbox VPC** contains only Private Subnets — **no Internet Gateway, no NAT Gateway**
- The EC2 instance running the AI model sits entirely inside
- It connects to AWS services through 3 VPC Endpoints:
  - **S3 Gateway Endpoint**: For EC2 to read files for analysis and write results (free)
  - **DynamoDB Gateway Endpoint**: For writing scan history to the database (free)
  - **CloudWatch Logs Interface Endpoint**: For logging AI progress (~$7/month for 1 AZ)


## Mistakes We Made


### Mistake 1: Forgot to enable Private DNS for Interface Endpoint


When creating the Interface Endpoint for CloudWatch Logs, we forgot to tick the **"Enable Private DNS Name"** checkbox. As a result, the Boto3 SDK inside EC2 still tried to resolve `logs.ap-southeast-1.amazonaws.com` to a public IP → timeout → no logs written.


**Fix:** Enable Private DNS in the endpoint configuration. Note: The VPC must have `enableDnsSupport` and `enableDnsHostnames` turned on first.


### Mistake 2: Security Group on Interface Endpoint blocking traffic


The Interface Endpoint creates an ENI, and that ENI has its own Security Group. We forgot to open port **443 (HTTPS)** on that ENI → EC2 couldn't reach the API.


**Fix:** Create a Security Group for the endpoint that allows inbound TCP 443 from the Sandbox subnet CIDR.


### Mistake 3: S3 Gateway Endpoint attached to the wrong Route Table


Gateway Endpoints work through route tables. We created the endpoint but attached it to the Main Route Table, while our EC2's subnet was using a separate Custom Route Table.


**Fix:** When creating the S3 Gateway Endpoint, select the exact route table that the subnet is associated with.


## Real-World Costs


| Endpoint | Type | Cost/Month |
|---|---|---|
| S3 | Gateway | **$0.00** |
| DynamoDB | Gateway | **$0.00** |
| CloudWatch Logs | Interface | **~$7.20** (1 AZ) |
| **Total** | | **~$7.20/month** |


If only active during testing (around 2 hours/day), costs drop to roughly **$0.60/month**.


## Lessons Learned


VPC Endpoints are a **must-have** component if you want to run any workload in a private subnet that still needs to interact with AWS services. Here's what we took away:


1. **Always prioritize Gateway Endpoints** for S3 and DynamoDB — they're free
2. **Check Private DNS immediately** after creating an Interface Endpoint — this is the #1 cause of connectivity failures
3. **The ENI's Security Group** is easy to overlook — remember to open port 443
4. **Route Tables must match** — especially when using custom route tables for subnets


Hopefully this post helps you avoid the same pitfalls we stumbled into. If you're building a sandbox, an isolated workload, or any system that needs private connectivity on AWS — VPC Endpoints are the first thing you should look into.


---


📎 **Further Reading:**
- [AWS Documentation — VPC Endpoints](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html)
- [AWS PrivateLink Pricing](https://aws.amazon.com/privatelink/pricing/)
