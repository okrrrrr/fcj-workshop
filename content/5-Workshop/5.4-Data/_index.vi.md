---
title : "Database & CI/CD Engineer"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

### Database & CI/CD Engineer

Sau khi hoàn thành việc xây dựng Frontend và Serverless Backend, bước tiếp theo là triển khai hệ thống lưu trữ dữ liệu và xây dựng quy trình tự động hóa triển khai ứng dụng (CI/CD). Trong phần này, hệ thống sử dụng Amazon S3 để lưu trữ các tệp được tải lên, đồng thời cấu hình Lifecycle Rule nhằm tối ưu chi phí lưu trữ và quản lý vòng đời dữ liệu.

Bên cạnh đó, quy trình Continuous Integration và Continuous Deployment (CI/CD) được xây dựng bằng các dịch vụ AWS như CodeBuild và CodePipeline. Quy trình này giúp tự động biên dịch, kiểm tra và triển khai ứng dụng mỗi khi mã nguồn được cập nhật từ GitHub, giảm thiểu thao tác thủ công và đảm bảo quá trình phát triển diễn ra nhanh chóng, chính xác và nhất quán.

Nội dung của phần này được chia thành bốn nội dung chính như sau:

- **5.4.1. Cấu hình Amazon S3 và Lifecycle Rule:** Tạo Bucket lưu trữ dữ liệu và cấu hình Lifecycle Rule để quản lý vòng đời của các tệp.
- **5.4.2. Chuẩn bị môi trường CI/CD:** Xây dựng tệp buildspec.yml, cấu hình quá trình Build và đưa mã nguồn lên GitHub.
- **5.4.3. Xây dựng AWS CodeBuild:** Tạo dự án CodeBuild và cấu hình môi trường Build để tự động biên dịch ứng dụng.
- **5.4.4. Xây dựng AWS CodePipeline:** Tạo Pipeline, kết nối GitHub với CodeBuild và cấu hình quy trình tự động triển khai ứng dụng.

![Data & CI/CD](/images/5-Workshop/5.4-Data/image.png)