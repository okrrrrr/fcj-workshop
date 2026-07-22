---
title: "Week 10 Worklog"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Objectives:

* Learn Cost Optimization: Cost Explorer, Budgets, Savings Plans.
* Learn how to monitor and control AWS costs.
* Practice right-sizing and optimization strategies.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Security Hub, IAM Identity Center from Week 9. Learned about AWS Cost Explorer: cost reports, charts to visualize spending. Understood cost allocation tags and usage by service to allocate costs. Learned Reserved Instances vs On-Demand vs Savings Plans tradeoffs | 22/06/2026 | 22/06/2026 | <https://docs.aws.amazon.com/cost-management/latest/userguide/ce-getting-started.html> |
| 3 | Accessed Cost Explorer Console to view costs. Viewed Cost & Usage by Service to identify top 5 most expensive services. Filtered by tag (Environment, Project, Team) to analyze costs by group. Viewed cost trend over time (daily, monthly) to understand patterns. Created custom cost report with specific filters to analyze specific areas. Downloaded report as CSV/Excel to share with team. Scheduled report delivery via email to receive regular updates. Enabled CUR (Cost & Usage Report) to have detailed cost data. Configured report prefix and s3 bucket to store reports. Set time granularity (Hourly) to have detailed breakdowns. Enabled resource IDs to track individual resource costs | 23/06/2026 | 23/06/2026 | <https://aws.amazon.com/aws-cost-management/aws-cost-explorer/getting-started/> |
| 4 | Accessed Budgets Console to set spending limits. Created Cost Budget with threshold ($100/month) to limit spending. Configured alert thresholds (50%, 80%, 100%) to receive early warnings. Added SNS topic for alerts to notify team when approaching limits. Created Usage Budget (EC2 hours, Lambda invocations) to track usage. Created RI Utilization Budget to track Reserved Instance coverage. Verified alerts trigger at correct threshold. Enabled Cost Anomaly Detection to identify unusual spending patterns. Created subscription (SNS topic) to receive anomaly alerts. Created monitor (single service or entire account) to track specific areas. Set sensitivity level to control alert frequency | 24/06/2026 | 24/06/2026 | <https://000007.awsstudygroup.com/> |
| 5 | Accessed Trusted Advisor Dashboard to view recommendations. Reviewed Cost Optimization checks to identify savings opportunities. Reviewed Security checks (MFA, IAM, public S3) to improve security posture. Reviewed Fault Tolerance checks to ensure high availability. Reviewed Performance checks to optimize resource usage. Downloaded TA report to share with stakeholders. Enabled Compute Optimizer to get recommendations. Reviewed EC2 instance recommendations to right-size instances. Reviewed EBS volume recommendations to optimize storage. Reviewed Lambda function recommendations to optimize serverless. Exported recommendations as CSV to plan implementation | 25/06/2026 | 25/06/2026 | <https://aws.amazon.com/trustedadvisor/getting-started/> |
| 6 | Analyzed current usage patterns in Cost Explorer to understand baseline. Calculated potential savings with Savings Plans to compare options. Purchased Compute Savings Plans (1-year, no upfront) to lock in savings. Reviewed RI recommendations from Trusted Advisor to consider Reserved Instances. Compared Savings Plans vs RI tradeoff to choose best option. Tagged all resources with consistent tagging strategy to enable cost allocation. Enabled CUR with resource IDs to track detailed costs. Set up Cost Budgets with alerts to prevent overspending. Reviewed Compute Optimizer recommendations to right-size resources. Implemented Reserved Instances/Savings Plans to reduce costs. Scheduled monthly cost review meetings to continuously optimize | 26/06/2026 | 26/06/2026 | <https://000042.awsstudygroup.com/> |


### Week 10 Achievements:

* Used Cost Explorer to analyze AWS costs.
* Created Budgets and alerts to monitor spending.
* Applied right-sizing recommendations from Compute Optimizer.
* Deployed Savings Plans and Reserved Instances to save costs.
