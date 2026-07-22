---
title : "Xây dựng Serverless Backend"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---

### Xây dựng Serverless Backend

Trong phần này, tiến hành xây dựng hệ thống **Serverless Backend** trên nền tảng Amazon Web Services (AWS) nhằm xử lý toàn bộ quy trình phân tích tệp tin được tải lên từ ứng dụng Frontend. Kiến trúc Serverless được triển khai bằng cách kết hợp nhiều dịch vụ AWS như **AWS Lambda**, **Amazon DynamoDB**, **Amazon SQS**, **AWS Step Functions** và **Identity and Access Management (IAM)** để xây dựng một quy trình xử lý tự động, không cần quản lý máy chủ.

Quy trình hoạt động của hệ thống bắt đầu khi người dùng tải tệp lên Amazon S3. Sự kiện từ S3 sẽ tự động kích hoạt các hàm Lambda để tiếp nhận yêu cầu, cập nhật trạng thái xử lý, gửi thông tin vào hàng đợi Amazon SQS và điều phối quá trình phân tích thông qua AWS Step Functions. Trong suốt quá trình xử lý, trạng thái của từng tệp sẽ được lưu trữ trên Amazon DynamoDB và đồng bộ với giao diện người dùng. Sau khi hoàn tất quá trình phân tích, hệ thống sẽ trả về kết quả để người dùng theo dõi trực tiếp trên website.

Nội dung workshop được chia thành các phần chính gồm chuẩn bị mã nguồn Backend, cấu hình các dịch vụ AWS, xây dựng quy trình xử lý bằng Step Functions và kiểm thử toàn bộ hệ thống.

Để thuận tiện cho việc triển khai và theo dõi, nội dung của phần **Xây dựng Serverless Backend** được chia thành bốn nội dung chính như sau:

- **5.3.1. Chuẩn bị mã nguồn Backend và tạo Amazon DynamoDB:** Chuẩn bị mã nguồn Backend, đóng gói các AWS Lambda Function và tạo cơ sở dữ liệu Amazon DynamoDB để lưu trữ thông tin xử lý.
- **5.3.2. Cấu hình Amazon SQS và AWS Lambda:** Tạo hàng đợi Amazon SQS, cấu hình IAM Role, triển khai các Lambda Function và thiết lập các Trigger giữa Amazon S3, Amazon SQS và AWS Lambda.
- **5.3.3. Xây dựng AWS Step Functions:** Tạo State Machine, cấu hình IAM Role và xây dựng quy trình điều phối các Lambda Function để thực hiện quá trình phân tích tự động.
- **5.3.4. Kiểm thử hệ thống:** Khởi chạy hệ thống, thực hiện tải tệp lên website, theo dõi trạng thái xử lý và kiểm tra kết quả trên Amazon DynamoDB cũng như giao diện người dùng.

![Serverless Backend](/images/5-Workshop/5.3-Serverless-Backend-Developer/image.png)