---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Tìm hiểu Cost Optimization: Cost Explorer, Budgets, Savings Plans.
* Học cách monitor và control chi phí AWS.
* Thực hành right-sizing và optimization strategies.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Security Hub, IAM Identity Center từ tuần 9. Tìm hiểu AWS Cost Explorer: cost reports, charts để visualize spending. Hiểu cost allocation tags và usage by service để phân bổ chi phí. Tìm hiểu Reserved Instances vs On-Demand vs Savings Plans tradeoffs | 22/06/2026 | 22/06/2026 | <https://docs.aws.amazon.com/cost-management/latest/userguide/ce-getting-started.html> |
| 3 | Truy cập Cost Explorer Console để xem chi phí. Xem Cost & Usage by Service để identify top 5 services tiêu nhiều nhất. Filter by tag (Environment, Project, Team) để phân tích chi phí theo nhóm. Xem cost trend over time (daily, monthly) để hiểu patterns. Tạo custom cost report với specific filters để analyze specific areas. Download report as CSV/Excel để share với team. Schedule report delivery via email để nhận regular updates. Enable CUR (Cost & Usage Report) để có detailed cost data. Configure report prefix và s3 bucket để store reports. Set time granularity (Hourly) để có detailed breakdowns. Enable resource IDs để track individual resource costs | 23/06/2026 | 23/06/2026 | <https://aws.amazon.com/aws-cost-management/aws-cost-explorer/getting-started/> |
| 4 | Truy cập Budgets Console để set spending limits. Tạo Cost Budget với threshold ($100/tháng) để limit spending. Cấu hình alert thresholds (50%, 80%, 100%) để nhận early warnings. Add SNS topic cho alerts để notify team khi approach limits. Tạo Usage Budget (EC2 hours, Lambda invocations) để track usage. Tạo RI Utilization Budget để track Reserved Instance coverage. Verify alerts trigger đúng threshold. Enable Cost Anomaly Detection để identify unusual spending patterns. Create subscription (SNS topic) để receive anomaly alerts. Create monitor (single service hoặc entire account) để track specific areas. Set sensitivity level để control alert frequency | 24/06/2026 | 24/06/2026 | <https://000007.awsstudygroup.com/> |
| 5 | Truy cập Trusted Advisor Dashboard để xem recommendations. Review Cost Optimization checks để identify savings opportunities. Review Security checks (MFA, IAM, public S3) để improve security posture. Review Fault Tolerance checks để ensure high availability. Review Performance checks để optimize resource usage. Download TA report để share với stakeholders. Enable Compute Optimizer để get recommendations. Review EC2 instance recommendations để right-size instances. Review EBS volume recommendations để optimize storage. Review Lambda function recommendations để optimize serverless. Export recommendations as CSV để plan implementation | 25/06/2026 | 25/06/2026 | <https://aws.amazon.com/trustedadvisor/getting-started/> |
| 6 | Analyze current usage patterns trong Cost Explorer để understand baseline. Tính toán potential savings với Savings Plans để compare options. Purchase Compute Savings Plans (1-year, no upfront) để lock in savings. Review RI recommendations từ Trusted Advisor để consider Reserved Instances. Compare Savings Plans vs RI tradeoff để choose best option. Tag all resources với consistent tagging strategy để enable cost allocation. Enable CUR với resource IDs để track detailed costs. Setup Cost Budgets với alerts để prevent overspending. Review Compute Optimizer recommendations để right-size resources. Implement Reserved Instances/Savings Plans để reduce costs. Schedule monthly cost review meetings để continuously optimize | 26/06/2026 | 26/06/2026 | <https://000042.awsstudygroup.com/> |


### Kết quả đạt được tuần 10:

* Sử dụng Cost Explorer để phân tích chi phí AWS.
* Tạo Budgets và alerts để monitor chi tiêu.
* Áp dụng right-sizing recommendations từ Compute Optimizer.
* Triển khai Savings Plans và Reserved Instances để tiết kiệm chi phí.
