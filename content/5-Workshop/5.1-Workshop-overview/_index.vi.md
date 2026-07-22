---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.1. </b> "
---

#### Giới thiệu về nền tảng Cloud phân tích và phát hiện mã độc tự động trên AWS

Trong workshop này, hệ thống được xây dựng nhằm triển khai một nền tảng **Cloud phân tích và phát hiện mã độc tự động** trên nền tảng **Amazon Web Services (AWS)**. Hệ thống được thiết kế theo kiến trúc **Serverless** kết hợp với các dịch vụ điện toán đám mây của AWS nhằm tự động hóa quá trình tiếp nhận, phân tích và quản lý các tệp được tải lên từ người dùng.

Ứng dụng được triển khai theo mô hình nhiều tầng, trong đó giao diện người dùng được phát triển bằng **React** và sử dụng **Amazon Cognito** để xác thực người dùng. Các tệp được tải lên **Amazon S3**, sau đó kích hoạt chuỗi xử lý tự động thông qua **AWS Lambda**, **Amazon SQS** và **AWS Step Functions**. Trạng thái xử lý được lưu trữ trên **Amazon DynamoDB**, đồng thời kết quả phân tích được đồng bộ và hiển thị trên giao diện Web. Bên cạnh đó, hệ thống còn tích hợp quy trình **CI/CD** bằng **AWS CodeBuild** và **AWS CodePipeline**, kết hợp với các dịch vụ bảo mật như **AWS WAF**, **IAM**, **AWS Secrets Manager**, **AWS KMS**, **AWS CloudTrail**, **AWS Config** và **Amazon VPC Endpoint** nhằm đảm bảo khả năng bảo mật, quản lý và giám sát toàn bộ hệ thống.

#### Tổng quan về Workshop

Trong workshop này, tiến hành triển khai nền tảng Cloud phân tích và phát hiện mã độc tự động trên AWS thông qua các nội dung chính sau:

+ Xây dựng giao diện Web bằng React, cấu hình Amazon Cognito, Amazon S3, Identity Pool và IAM Role để xác thực người dùng và quản lý việc tải tệp lên hệ thống.

+ Triển khai Serverless Backend sử dụng AWS Lambda, Amazon DynamoDB, Amazon SQS và AWS Step Functions nhằm tự động xử lý và phân tích các tệp được tải lên.

+ Xây dựng cơ sở dữ liệu, cấu hình Amazon S3 Lifecycle Rule và triển khai quy trình **Continuous Integration/Continuous Deployment (CI/CD)** bằng AWS CodeBuild và AWS CodePipeline.

+ Triển khai các cơ chế bảo mật trên AWS bao gồm IAM OIDC Provider, GitHub Actions, AWS WAF, AWS Secrets Manager, AWS Key Management Service (KMS), AWS CloudTrail và AWS Config nhằm tăng cường khả năng bảo vệ, quản lý và giám sát hệ thống.

+ Xây dựng kết nối Hybrid an toàn giữa Amazon VPC và Amazon S3 bằng Amazon VPC Endpoint, giúp các tài nguyên trong VPC truy cập các dịch vụ AWS thông qua mạng nội bộ mà không cần đi qua Internet công cộng.


![Tổng quan Workshop](/images/5-Workshop/5.1-Workshop-overview/diagram1.png)
