---
title: "Worklog Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Tìm hiểu các dịch vụ Monitoring và Logging: CloudWatch, CloudTrail.
* Học cách sử dụng AWS Config để quản lý compliance.
* Thực hành thiết lập hệ thống giám sát cho ứng dụng.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Auto Scaling, Load Balancer từ tuần 3. Tìm hiểu CloudWatch: metrics, alarms, dashboards, logs. Tìm hiểu CloudWatch Logs Insights để query logs phức tạp. Hiểu metric filters và subscription filters | 11/05/2026 | 11/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Truy cập CloudWatch Console. Tạo Dashboard mới với các widget hiển thị CPU, Memory, Network metrics. Tạo Alarm cho CPU Utilization > 80%. Tạo Alarm cho Disk Space < 20%. Cấu hình SNS Topic với subscription email để nhận notification khi alarm trigger. Cài đặt CloudWatch Agent trên EC2 để thu thập custom metrics. Cấu hình logs từ Apache xem trong CloudWatch Logs | 12/05/2026 | 12/05/2026 | <https://000008.awsstudygroup.com/vi/> |
| 4 | Truy cập CloudTrail Console. Tạo Trail mới cấu hình gửi logs đến S3 Bucket riêng. Enable CloudWatch Logs integration để phân tích logs. Tạo bucket policy cho CloudTrail access. Thực hiện các thao tác AWS (tạo EC2, S3) để tạo events. Kiểm tra Event History xem tất cả API calls đã thực hiện. Tải và phân tích log file từ S3 để hiểu cấu trúc JSON log | 13/05/2026 | 13/05/2026 | <https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-getting-started.html> |
| 5 | Truy cập AWS Config Console. Bật AWS Config và chọn S3 bucket để lưu configuration history. Chọn IAM Role cho AWS Config. Xem Resource inventory để thấy danh sách tất cả resources trong tài khoản. Tạo Config Rule tùy chỉnh (ví dụ: require encrypted S3 buckets). Xem compliance status của EC2 instances. Tạo CloudWatch Event rule để phản hồi tự động khi có non-compliance. Truy cập Systems Manager Console. Tạo Document để chạy commands trên EC2. Sử dụng Run Command để cài software trên nhiều instances cùng lúc thay vì SSH vào từng máy | 14/05/2026 | 14/05/2026 | <https://docs.aws.amazon.com/config/latest/developerguide/WhatIsConfig.html> |
| 6 | Tạo VPC với Public và Private Subnets. Launch EC2 instances với Auto Scaling Group. Cấu hình CloudWatch Dashboard theo dõi all metrics tập trung tại một nơi. Thiết lập CloudWatch Alarms cho tất cả services quan trọng. Enable CloudTrail để log all API calls phục vụ audit. Enable AWS Config để track resource changes và compliance. Tạo SNS Topic với subscription để nhận alerts khi có sự cố. Tạo CloudWatch Composite Alarm kết hợp nhiều metrics. Test bằng cách tạo load cao verify alarms trigger đúng. Kiểm tra CloudTrail logs để verify audit trail đầy đủ | 15/05/2026 | 15/05/2026 | <https://000008.awsstudygroup.com/vi/> |


### Kết quả đạt được tuần 4:

* Tạo và cấu hình CloudWatch Dashboard theo dõi metrics của ứng dụng.
* Thiết lập CloudWatch Alarms và SNS notifications cho alerts.
* Enable và sử dụng CloudTrail để audit API calls.
* Cấu hình AWS Config để track resource compliance.
* Sử dụng Systems Manager để quản lý EC2 instances hiệu quả.
