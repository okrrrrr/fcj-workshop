---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Learn Security & Compliance: IAM Identity Center, Organizations.
* Learn how to manage multi-account with Control Tower.
* Practice Security Hub and compliance automation.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Redshift, Glue, Athena from Week 8. Learned about IAM Identity Center (formerly SSO): SSO, permission sets. Understood AWS Organizations: OU structure, SCPs to control permissions. Learned consolidated billing and cross-account access | 15/06/2026 | 15/06/2026 | <https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html> |
| 3 | Enabled IAM Identity Center for Single Sign-On. Configured identity source (AWS managed or connect with Active Directory). Created Permission Sets with different roles (Admin, Developer, ReadOnly) to control access levels. Assigned permission set to AWS account to grant permissions. Added users and groups to manage access. Logged in via SSO portal URL to test. Tested access with different permission sets to verify permissions work correctly. Created organization with management account to manage all accounts. Created OU (Organizational Units): Production, Development, Security to group accounts by purpose | 16/06/2026 | 16/06/2026 | <https://000012.awsstudygroup.com/> |
| 4 | Enabled all features in Organizations to use SCPs. Created SCP to deny unauthorized regions (e.g., block us-east-1). Created SCP to require encryption on S3 buckets. Attached SCPs to OU levels to apply policies for entire groups. Tested SCP effect with member account to verify blocking works. Verified SCP blocking unauthorized actions as expected. Understood Landing Zone architecture to setup multi-account environment. Learned about Account Factory to standardize account creation. Understood preventive guardrails (prevent) and detective guardrails (detect) to enforce compliance | 17/06/2026 | 17/06/2026 | <https://000012.awsstudygroup.com/> |
| 5 | Enabled Security Hub (manual or CloudFormation) to centralize security findings. Enabled security standards like CIS, PCI DSS, AWS Foundational to check compliance. Enabled integrations with GuardDuty, Config, Macie to aggregate findings. Reviewed findings from enabled standards to identify issues. Created custom insight to track specific important findings. Investigated and acknowledged findings to resolve security issues. Set up CloudWatch Event rule to notify when new findings appear. Enabled AWS Config recording to track resource changes. Created conformance pack to bundle compliance rules. Reviewed compliance status to see overall compliance score | 18/06/2026 | 18/06/2026 | <https://www.pluralsight.com/labs/aws/implementing-aws-security-hub> |
| 6 | Enabled IAM Access Analyzer for account to identify external access. Reviewed external access findings (S3 buckets, IAM roles) to identify unintended access. Analyzed resource policies to understand permissions granted. Created archive rule for findings not needing investigation to reduce noise. Generated policy from findings to review and refine permissions. Set up AWS Audit Manager to automate evidence collection. Selected framework (CIS, GDPR, HIPAA) based on compliance requirements. Created custom assessment to fit organizational needs. Reviewed automated evidence collection to verify coverage. Generated compliance report to present to auditors | 19/06/2026 | 19/06/2026 | <https://docs.aws.amazon.com/access-analyzer/> |


### Week 9 Achievements:

* Configured IAM Identity Center for Single Sign-On.
* Managed multi-account with AWS Organizations and SCPs.
* Deployed Security Hub and compliance monitoring.
* Used IAM Access Analyzer to analyze external access.
* Used Audit Manager to generate compliance reports.
