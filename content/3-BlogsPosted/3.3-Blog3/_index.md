---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
{{% notice warning %}}
⚠️ **Note:** The information below is for reference purposes only. Please **do not copy verbatim** for your report, including this warning.
{{% /notice %}}

# AWS CONFIG AUTO-REMEDIATION — AUTOMATICALLY LOCK AN S3 BUCKET WITHIN 1 SECOND IF SOMEONE ACCIDENTALLY MAKES IT PUBLIC


## It Started with a Mistake


I always thought "accidentally enabling Public Access on an S3 bucket" only happened in tutorials — no one would do that in real life. Until I was testing CORS for our file upload system, went into the S3 console, unticked **Block Public Access** to debug... and forgot to turn it back on.


Luckily, the bucket had no real data at the time. But in our malware analysis system, the S3 bucket stores suspected malware files — if that went public, the consequences would be severe. From that moment, I decided: **there must be an automatic mechanism to lock it back immediately, without depending on humans**.


The solution I chose was the trio: **AWS Config + EventBridge + Lambda**.


## What is AWS Config?


AWS Config is a service that monitors the configuration of resources on AWS. It continuously tracks and evaluates whether your resources comply with the "rules" you define.


For example: you can set a rule saying **"All S3 buckets must have Block Public Access enabled"**. Whenever someone changes an S3 configuration, Config re-evaluates and marks the bucket as **COMPLIANT** or **NON_COMPLIANT**.


But Config only **detects** — it doesn't fix anything. To automatically remediate, we need EventBridge and Lambda.


## Auto-Remediation Architecture


![Auto-Remediation Architecture](/images/3-Blog/blog3_auto_remediation.png)


Here's how the flow works:


1. **Someone enables Public Access** on an S3 bucket (accidentally or intentionally)
2. **AWS Config** detects the change and evaluates the bucket as **NON_COMPLIANT** against the `s3-bucket-public-read-prohibited` rule
3. **EventBridge Rule** catches the compliance change event from Config
4. **Lambda function** is triggered, calling the `PutPublicAccessBlock` API to lock the bucket immediately
5. **S3 bucket** returns to a secure state — the entire process takes **less than 1 second**


## Step-by-Step Setup


### Step 1: Create the AWS Config Rule


Go to AWS Config → Rules → Add rule → select **Managed rule**:
- Rule name: `s3-bucket-public-read-prohibited`
- Trigger: Configuration changes
- Scope: Resources — `AWS::S3::Bucket`


This rule automatically evaluates whenever any configuration change occurs on any S3 bucket.


### Step 2: Create the Lambda Remediation Function


```python
import boto3
import json


s3_client = boto3.client('s3')


def lambda_handler(event, context):
    """
    Auto-remediation: When EventBridge notifies that an S3 bucket 
    is NON_COMPLIANT, automatically Block Public Access.
    """
    detail = event.get('detail', {})
    
    # Get bucket name from event
    resource_id = detail.get('resourceId', '')
    compliance = detail.get('newEvaluationResult', {}).get('complianceType', '')
    
    if compliance != 'NON_COMPLIANT':
        print(f"Bucket {resource_id} is compliant. No action needed.")
        return
    
    print(f"⚠️ Bucket {resource_id} is NON_COMPLIANT! Remediating...")
    
    try:
        # Block Public Access immediately
        s3_client.put_public_access_block(
            Bucket=resource_id,
            PublicAccessBlockConfiguration={
                'BlockPublicAcls': True,
                'IgnorePublicAcls': True,
                'BlockPublicPolicy': True,
                'RestrictPublicBuckets': True
            }
        )
        print(f"✅ Successfully blocked public access for bucket: {resource_id}")
        
    except Exception as e:
        print(f"❌ Failed to remediate bucket {resource_id}: {str(e)}")
        raise e
```


IAM Role for Lambda needs these permissions:
```json
{
  "Effect": "Allow",
  "Action": [
    "s3:PutBucketPublicAccessBlock",
    "s3:GetBucketPublicAccessBlock"
  ],
  "Resource": "arn:aws:s3:::*"
}
```


### Step 3: Create the EventBridge Rule


Go to EventBridge → Create rule:
- **Event pattern:**
```json
{
  "source": ["aws.config"],
  "detail-type": ["Config Rules Compliance Change"],
  "detail": {
    "messageType": ["ComplianceChangeNotification"],
    "configRuleName": ["s3-bucket-public-read-prohibited"],
    "newEvaluationResult": {
      "complianceType": ["NON_COMPLIANT"]
    }
  }
}
```
- **Target:** Lambda function from Step 2


### Step 4: Test It


1. Go to any S3 bucket → Permissions → disable Block Public Access
2. Wait about 30-60 seconds (time for Config to evaluate)
3. Check again → Block Public Access has been automatically re-enabled ✅
4. Check CloudWatch Logs for the Lambda → you'll see `"Successfully blocked public access"`


## Comparison: Manual vs Automated


| Criteria | Manual Handling | Auto-Remediation |
|---|---|---|
| Detection time | Hours to days | **< 1 minute** |
| Fix time | Depends on humans | **< 1 second** (after detection) |
| Reliability | Easy to forget or miss | **100% automated** |
| After-hours coverage | No (unless someone is on-call) | **24/7** |
| Cost | Staff time | ~$1/month (Config rule) |


## Extending the Pattern


Beyond S3 Public Access, we applied the same pattern for:


- **Security Group with port 22 open to 0.0.0.0/0** → automatically remove the rule
- **Unencrypted EBS volumes** → automatically create encrypted snapshots
- **IAM Access Keys older than 90 days** → automatically send alerts via SNS


All use the same architecture: **Config Rule → EventBridge → Lambda**.


## Lessons Learned


1. **Humans will always make mistakes** — don't rely on manual checklists for security
2. **AWS Config + EventBridge + Lambda** is the golden trio for auto-remediation
3. **Costs are minimal** — about $1-2/month for a few Config rules, in exchange for absolute peace of mind
4. **Log everything** — record who changed what, what Lambda fixed, for future audit purposes
5. **Test before you trust** — always try breaking a rule and verify Lambda fixes it


This is probably one of the things I'm most proud of in our internship project. Not because it's complex, but because it solves a real-world problem that even large teams still face: **human error in cloud security configuration**.


---


📎 **Further Reading:**
- [AWS Documentation — AWS Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html)
- [AWS Documentation — Remediating Noncompliant Resources](https://docs.aws.amazon.com/config/latest/developerguide/remediation.html)
- [AWS Blog — Auto-Remediate Non-Compliant AWS Resources](https://aws.amazon.com/blogs/mt/auto-remediate-non-compliant-aws-resources/)
