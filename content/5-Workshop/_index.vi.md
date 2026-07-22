---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

### Tổng quan

Trong workshop này, tiến hành xây dựng một **nền tảng Cloud phân tích và phát hiện mã độc tự động trên nền tảng Amazon Web Services (AWS)** theo kiến trúc Serverless. Hệ thống cho phép người dùng tải tệp cần kiểm tra thông qua giao diện Web, sau đó tự động thực hiện quá trình phân tích, xử lý và trả về kết quả trên môi trường điện toán đám mây.

Để xây dựng hệ thống hoàn chỉnh, nhiều dịch vụ của AWS được tích hợp nhằm đảm nhiệm các chức năng khác nhau. Giao diện người dùng được phát triển bằng React và xác thực thông qua Amazon Cognito. Các tệp được lưu trữ trên Amazon S3 và toàn bộ quy trình xử lý được thực hiện bằng AWS Lambda kết hợp với Amazon SQS, Amazon DynamoDB và AWS Step Functions theo kiến trúc Serverless.

Bên cạnh đó, hệ thống còn triển khai quy trình **Continuous Integration và Continuous Deployment (CI/CD)** bằng AWS CodeBuild và AWS CodePipeline nhằm tự động hóa quá trình xây dựng và triển khai ứng dụng. Đồng thời, các cơ chế bảo mật như IAM, AWS WAF, AWS Secrets Manager, AWS KMS, AWS CloudTrail và AWS Config cũng được cấu hình để tăng cường khả năng bảo vệ hệ thống, quản lý quyền truy cập, lưu trữ thông tin nhạy cảm và giám sát toàn bộ hoạt động của các tài nguyên trên AWS.

Cuối cùng, giải pháp **Amazon VPC Endpoint** được triển khai để xây dựng kết nối riêng tư giữa Amazon Virtual Private Cloud (Amazon VPC) và Amazon S3, giúp các tài nguyên trong hệ thống truy cập dịch vụ AWS thông qua mạng nội bộ mà không cần đi qua Internet công cộng, từ đó nâng cao tính bảo mật và hiệu năng của toàn bộ nền tảng.

### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Web Frontend Developer](5.2-Web-Frontend-Developer/)
3. [Serverless Backend Developer](5.3-Serverless-Backend-Developer/)
4. [Data](5.4-Data/)
5. [AI Security Analyst & Web Admin](5.5-AI-Security-Analyst-%26-Web-Admin/)
6. [Perimeter Security & Cloud Admin](5.6-Perimeter%20Security%20%26%20Cloud%20Admin/)