---
title: "Worklog Tuần 3"
date: 2026-05-04
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Tìm hiểu Auto Scaling và Elastic Load Balancing (ELB).
* Học cách sử dụng DynamoDB - database NoSQL của AWS.
* Thực hành triển khai ứng dụng với Load Balancer và Auto Scaling.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập VPC, Security Group từ tuần 1-2. Tìm hiểu Auto Scaling: tại sao cần tự động scale instance. Tìm hiểu ELB: phân biệt Application LB vs Network LB vs Gateway LB | 04/05/2026 | 04/05/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | Tạo Launch Template với EC2 (Amazon Linux 2 AMI). Cấu hình User Data tự động cài Apache. Tạo Target Group cho Load Balancer. Tạo Application Load Balancer (ALB) với Security Group mở port 80/443. Khởi tạo Auto Scaling Group với min=1, max=3 instances. Cấu hình Scaling Policy dựa trên CPU Utilization target 70%. Test Auto Scaling bằng load test | 05/05/2026 | 05/05/2026 | <https://000006.awsstudygroup.com/> |
| 4 | Truy cập DynamoDB Console. Tạo Table mới với Partition Key (user_id). Chọn Capacity Mode (On-Demand hoặc Provisioned). Thêm items vào table (user_id, name, email). Tạo Global Secondary Index (GSI) để query theo email. Bật Point-in-time Recovery (PITR). Tạo On-Demand Backup cho table. Kết nối DynamoDB từ Lambda function | 06/05/2026 | 06/05/2026 | <https://000060.awsstudygroup.com/> |
| 5 | Tạo RDS Instance với MySQL (t2.micro). Bật Multi-AZ Deployment để tăng availability. Enable Encryption cho RDS Instance. Tạo Read Replica để phân chia đọc dữ liệu. Kết nối RDS từ EC2 bằng MySQL Client. Tạo Parameter Group tùy chỉnh (max_connections). Tạo Option Group để enable BACKUP. Tạo Secret lưu username/password RDS trong Secrets Manager. Cấu hình Lambda đọc secret từ Secrets Manager thay vì hardcode credentials | 07/05/2026 | 07/05/2026 | <https://000005.awsstudygroup.com/> |
| 6 | Thiết kế VPC với 2 Availability Zones (ap-southeast-1a, ap-southeast-1b). Tạo Public Subnet ở mỗi AZ cho ALB và Private Subnet cho EC2. Tạo NAT Gateway trong Public Subnet để Private subnet có internet. Launch EC2 instances trong Auto Scaling Group. Cấu hình Application Load Balancer phân phối traffic across 2 AZs. Tạo RDS với Multi-AZ trong Private Subnet đảm bảo database luôn available. Deploy web application lên EC2. Test failover bằng cách terminate một instance và verify website vẫn hoạt động qua ALB DNS | 08/05/2026 | 08/05/2026 | <https://000101.awsstudygroup.com/> |


### Kết quả đạt được tuần 3:

* Hiểu và triển khai thành công Auto Scaling Group với Load Balancer.
* Tạo và quản lý DynamoDB Table, sử dụng GSI và backup.
* Triển khai Web Application với High Availability (Multi-AZ).
* Cấu hình RDS Multi-AZ và Read Replica.
* Sử dụng Secrets Manager để quản lý credentials an toàn.
