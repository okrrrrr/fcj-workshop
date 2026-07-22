---
title: "Worklog Tuần 1"
date: 2026-04-20
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu tuần 1:

* Hoàn thành các thủ tục giấy tờ nhận AWS Credits từ FCAJ.
* Tìm hiểu tổng quan về Cloud Computing và hạ tầng AWS (Region, AZ, Edge Location).
* Nắm bắt kiến thức cơ bản về VPC, Subnet, Route Table, Internet Gateway, NAT Gateway.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Gặp gỡ anh chị trong team FCAJ, giới thiệu bản thân để làm quen, nhận thông tin tài khoản AWS và hướng dẫn sử dụng credits từ mentor, đọc và lưu ý các nội quy, quy định tại đơn vị thực tập, lên kế hoạch 12 tuần thực tập với milestones cụ thể | 20/04/2026 | 20/04/2026 | <https://app.notion.com/p/Group-description-TP-HCM-347df829a730809a8f63d39505644917> |
| 3 | Tìm hiểu AWS là gì và tại sao nên dùng Cloud (scalability, flexibility, cost-efficiency), tìm hiểu mô hình Region, Availability Zone, Edge Location để hiểu global infrastructure, phân biệt các loại dịch vụ AWS: Compute (EC2, Lambda), Storage (S3), Networking (VPC), Database (RDS), Security (IAM), Management (CloudWatch) | 21/04/2026 | 21/04/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | Tạo AWS Free Tier Account: Truy cập aws.amazon.com, click "Create an AWS Account", nhập email, password, chọn "Personal" account, nhập thông tin cá nhân và thẻ tín dụng để xác minh danh tính, xác minh số điện thoại qua cuộc gọi hoặc SMS, xác nhận email từ AWS, chọn Support Plan (Basic) để hoàn tất đăng ký. Cài đặt AWS CLI: Download AWS CLI v2 cho Windows từ aws.amazon.com/cli, chạy file cài đặt và làm theo hướng dẫn, mở Command Prompt kiểm tra version: aws --version, truy cập IAM Console → Users → tạo Access Key cho programmatic access, chạy aws configure nhập Access Key ID, Secret Access Key, region (ap-southeast-1), verify credentials bằng lệnh aws sts get-caller-identity | 22/04/2026 | 22/04/2026 | <https://000011.awsstudygroup.com/> |
| 5 | IAM Lab: Truy cập IAM Console, tạo IAM User đầu tiên với programmatic access, gán Policy trực tiếp cho user (ví dụ: AmazonEC2ReadOnlyAccess), tạo Group "Developers" để group users có cùng responsibilities, gán policy cho group thay vì gán trực tiếp cho user, add user vào group để kế thừa permissions, tạo Role cho EC2 với policy AmazonS3ReadOnlyAccess để EC2 có thể đọc S3. EC2 Lab: Tìm hiểu các Instance Types: t2 (general purpose), m5 (compute optimized), c5 (memory optimized), chọn AMI phù hợp: Amazon Linux 2, Ubuntu, hoặc Windows, tạo Key Pair trong EC2 Console và download .pem file để SSH, cấu hình Instance Details bao gồm VPC, Subnet, Security Group, Review và Launch Instance, kết nối SSH vào instance bằng PuTTY (Windows) hoặc Git Bash (Mac/Linux) | 23/04/2026 | 23/04/2026 | <https://000002.awsstudygroup.com/> |
| 6 | VPC Lab: Tạo VPC mới với CIDR block 10.0.0.0/16 để define IP range cho network, tạo Public Subnet với CIDR 10.0.1.0/24 trong Availability Zone đầu tiên, tạo Private Subnet với CIDR 10.0.2.0/24 để host private resources, tạo Internet Gateway (IGW) mới và đính vào VPC để enable internet access, tạo Route Table riêng cho public subnet, thêm route: Destination 0.0.0.0/0 → Target IGW để allow outbound traffic, associate public subnet với route table vừa tạo. Security Group & NACL Lab: Tạo Security Group cho EC2 với default deny policy, thêm Inbound Rule: SSH (port 22) cho maintenance, HTTP (port 80) và HTTPS (port 443) cho web traffic, tạo Network ACL với rule numbering (100, 200...) để control traffic at subnet level, associate NACL với subnet và understand difference giữa SG (stateful) và NACL (stateless) | 24/04/2026 | 24/04/2026 | <https://000003.awsstudygroup.com/> |


### Kết quả đạt được tuần 1:

* Hoàn thành thủ tục nhận AWS Credits, tài khoản AWS đã active.
* Cài đặt và cấu hình thành công AWS CLI trên máy local.
* Nắm được kiến thức cơ bản về IAM, EC2, EBS, VPC, S3.
* Tạo thành công VPC đầu tiên với Public và Private Subnet.
* Cấu hình được Internet Gateway và Route Table.
