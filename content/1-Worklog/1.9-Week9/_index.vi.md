---
title: "Worklog Tuần 9"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Tìm hiểu Security & Compliance: IAM Identity Center, Organizations.
* Học cách quản lý multi-account với Control Tower.
* Thực hành Security Hub và compliance automation.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Redshift, Glue, Athena từ tuần 8. Tìm hiểu IAM Identity Center (formerly SSO): SSO, permission sets. Hiểu AWS Organizations: OU structure, SCPs để control permissions. Tìm hiểu consolidated billing và cross-account access | 15/06/2026 | 15/06/2026 | <https://docs.aws.amazon.com/singlesignon/latest/userguide/what-is.html> |
| 3 | Enable IAM Identity Center để enable Single Sign-On. Configure identity source (AWS managed hoặc connect với Active Directory). Tạo Permission Sets với different roles (Admin, Developer, ReadOnly) để control access levels. Assign permission set đến AWS account để grant quyền. Add users và groups để manage access. Login qua SSO portal URL để test. Test access với different permission sets để verify permissions hoạt động đúng. Create organization với management account để quản lý tất cả accounts. Create OU (Organizational Units): Production, Development, Security để group accounts theo mục đích | 16/06/2026 | 16/06/2026 | <https://000012.awsstudygroup.com/> |
| 4 | Enable all features trong Organizations để sử dụng SCPs. Tạo SCP để deny region không được phép (ví dụ: block us-east-1). Tạo SCP để require encryption on S3 buckets. Attach SCPs to OU levels để apply policies cho entire groups. Test SCP effect với member account để verify blocking hoạt động. Verify SCP blocking unauthorized actions đúng như mong đợi. Hiểu Landing Zone architecture để setup multi-account environment. Tìm hiểu Account Factory để standardize account creation. Hiểu preventive guardrails (ngăn chặn) và detective guardrails (phát hiện) để enforce compliance | 17/06/2026 | 17/06/2026 | <https://000012.awsstudygroup.com/> |
| 5 | Enable Security Hub (thủ công hoặc CloudFormation) để centralize security findings. Enable security standards như CIS, PCI DSS, AWS Foundational để check compliance. Enable integrations với GuardDuty, Config, Macie để aggregate findings. Review findings từ enabled standards để identify issues. Tạo custom insight để track specific findings quan trọng. Investigate và acknowledge findings để resolve security issues. Setup CloudWatch Event rule để notify khi có new findings. Enable AWS Config recording để track resource changes. Tạo conformance pack để bundle compliance rules. Review compliance status để xem overall compliance score | 18/06/2026 | 18/06/2026 | <https://www.pluralsight.com/labs/aws/implementing-aws-security-hub> |
| 6 | Enable IAM Access Analyzer cho account để identify external access. Review external access findings (S3 buckets, IAM roles) để identify unintended access. Analyze resource policies để understand permissions đã granted. Tạo archive rule cho findings không cần investigate để reduce noise. Generate policy từ findings để review và refine permissions. Setup AWS Audit Manager để automate evidence collection. Select framework (CIS, GDPR, HIPAA) tùy theo compliance requirements. Create custom assessment để fit organizational needs. Review automated evidence collection để verify coverage. Generate compliance report để present to auditors | 19/06/2026 | 19/06/2026 | <https://docs.aws.amazon.com/access-analyzer/> |


### Kết quả đạt được tuần 9:

* Cấu hình IAM Identity Center cho Single Sign-On.
* Quản lý multi-account với AWS Organizations và SCPs.
* Triển khai Security Hub và compliance monitoring.
* Sử dụng IAM Access Analyzer để phân tích external access.
* Sử dụng Audit Manager để generate compliance reports.
