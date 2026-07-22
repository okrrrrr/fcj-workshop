---
title : "Perimeter Security & Cloud Admin"
date : 2024-01-01
weight : 11
chapter : false
pre : " <b> 5.6. </b> "
---

### Perimeter Security & Cloud Admin

Sau khi hoàn thiện hệ thống Frontend, Serverless Backend và quy trình CI/CD, bước tiếp theo là triển khai các cơ chế bảo mật và giám sát trên nền tảng Amazon Web Services (AWS). Mục tiêu của phần này là tăng cường khả năng bảo vệ hệ thống trước các truy cập trái phép, quản lý an toàn thông tin nhạy cảm, mã hóa dữ liệu và giám sát toàn bộ hoạt động của các tài nguyên trên môi trường Cloud.

Trong workshop, các dịch vụ như **AWS Identity and Access Management (IAM)**, **AWS WAF**, **AWS Secrets Manager**, **AWS Key Management Service (KMS)**, **AWS CloudTrail** và **AWS Config** được sử dụng để xây dựng một lớp bảo mật toàn diện. Các dịch vụ này giúp xác thực an toàn giữa GitHub Actions và AWS, bảo vệ API Gateway khỏi các cuộc tấn công, quản lý khóa mã hóa và thông tin bí mật, đồng thời ghi nhận và đánh giá trạng thái cấu hình của toàn bộ hệ thống.

Nội dung của phần này được chia thành bốn nội dung chính như sau:

- **5.6.1. Cấu hình IAM OIDC Provider và GitHub Actions:** Thiết lập cơ chế xác thực giữa GitHub Actions và AWS bằng OpenID Connect (OIDC), đồng thời tạo IAM Role để phục vụ quá trình triển khai tự động.
- **5.6.2. Cấu hình AWS WAF bảo vệ API Gateway:** Tạo Web ACL và cấu hình các Rule nhằm bảo vệ API Gateway trước các cuộc tấn công như DoS hoặc Spam Request.
- **5.6.3. Quản lý khóa mã hóa và thông tin bí mật:** Sử dụng AWS Secrets Manager để lưu trữ thông tin nhạy cảm và AWS KMS để quản lý khóa mã hóa dữ liệu.
- **5.6.4. Giám sát và đánh giá tuân thủ hệ thống:** Cấu hình AWS CloudTrail và AWS Config để ghi nhận nhật ký hoạt động, theo dõi thay đổi tài nguyên và đánh giá mức độ tuân thủ các chính sách bảo mật.

![Perimeter Security & Cloud Admin](/images/5-Workshop/5.6-Perimeter-Security/image.png)