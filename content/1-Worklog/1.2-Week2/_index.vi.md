---
title: "Worklog Tuần 2"
date: 2026-04-27
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Ôn tập IAM, EC2 từ tuần 1 và nắm vững kiến thức nền tảng.
* Tìm hiểu các dịch vụ quan trọng: Lambda (Serverless), S3, RDS, CloudWatch.
* Thực hành deploy web application hoàn chỉnh trên AWS.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập IAM tuần 1: Users, Groups, Roles, Policies. Tìm hiểu Lambda - mô hình Serverless khác gì EC2. Khi nào nên dùng Lambda, khi nào dùng EC2. Hiểu cách Lambda handle requests, cold start, pricing | 27/04/2026 | 27/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Tạo EC2 Instance (t2.micro, Amazon Linux 2), cấu hình Security Group mở port 22 (SSH) và port 80 (HTTP). Kết nối SSH bằng Git Bash. Cài đặt và cấu hình Apache web server, tự động khởi động service. Tạo và mount EBS volume để lưu dữ liệu | 28/04/2026 | 28/04/2026 | <https://000004.awsstudygroup.com/> |
| 4 | Tạo S3 Bucket với tên unique toàn cầu. Upload objects (file text, hình ảnh). Bật Versioning để theo dõi lịch sử thay đổi file. Tạo Lifecycle rule tự động chuyển dữ liệu sang Glacier sau 30 ngày. Cấu hình Static Website Hosting để host static site. Tạo Bucket Policy cho phép public read access | 29/04/2026 | 29/04/2026 | <https://000057.awsstudygroup.com/> |
| 5 | Tạo DB Subnet Group với ít nhất 2 subnet trong các Availability Zone khác nhau. Tạo Security Group cho RDS mở port 3306 (MySQL). Khởi tạo RDS Instance với MySQL engine (t2.micro), lưu lại endpoint và credentials để kết nối. Kết nối từ EC2 bằng MySQL Client. Tạo database, table và insert data để test. Truy cập CloudWatch Dashboard xem metrics. Tạo Alarm theo dõi CPU usage > 80%. Tạo SNS Topic và subscription để nhận thông báo qua email khi alarm trigger | 30/04/2026 | 30/04/2026 | <https://000005.awsstudygroup.com/> |
| 6 | Tạo Lambda Function đầu tiên với Python runtime. Viết handler code xử lý request đơn giản. Cấu hình API Gateway làm trigger để gọi Lambda qua HTTP. Test function và xem logs trong CloudWatch. Thực hành cấu hình Environment Variables và set Memory/Timeout. Thiết kế VPC với Public Subnet (chứa EC2) và Private Subnet (chứa RDS). Launch EC2 trong Public Subnet và cấu hình Internet Gateway. Launch RDS trong Private Subnet để bảo mật database. Cấu hình NAT Gateway để EC2 có thể download packages. Deploy web application lên EC2 và kết nối đến RDS | 01/05/2026 | 01/05/2026 | <https://000101.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Nắm vững kiến thức IAM, EC2, S3 qua thực hành lab.
* Hiểu rõ sự khác biệt giữa Serverless (Lambda) và Traditional (EC2).
* Tạo thành công RDS Instance và kết nối từ EC2.
* Triển khai Lambda Function đầu tiên với API Gateway trigger.
* Xây dựng hoàn chỉnh Web Application với VPC, EC2 và RDS.
