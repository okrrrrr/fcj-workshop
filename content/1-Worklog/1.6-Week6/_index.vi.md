---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tìm hiểu Serverless với Lambda và API Gateway.
* Học cách xây dựng event-driven architecture với EventBridge.
* Thực hành Step Functions để orchestrate workflows.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Docker, ECS từ tuần 5. Tìm hiểu Lambda cơ bản: functions, runtimes, triggers. Hiểu Lambda execution roles và environment variables. Tìm hiểu Lambda layers để share code và versioning | 25/05/2026 | 25/05/2026 | <https://serverlessland.com/lambda> |
| 3 | Tạo Lambda Function với Python runtime. Viết handler code xử lý event. Cấu hình API Gateway REST API mới. Tạo GET method với Lambda integration để lấy data. Tạo POST method để nhận data từ client. Deploy API sang Stage (dev) để test. Test API bằng Postman hoặc curl. Enable CORS cho API Gateway để cho phép cross-origin requests | 26/05/2026 | 26/05/2026 | <https://000066.awsstudygroup.com/> |
| 4 | Tạo DynamoDB Table (Users) với partition key user_id. Tạo Lambda function cho CREATE operation (POST /users) để thêm user mới. Tạo Lambda function cho READ operation (GET /users/{id}) để lấy thông tin user. Tạo Lambda function cho UPDATE operation (PUT /users/{id}) để cập nhật data. Tạo Lambda function cho DELETE operation (DELETE /users/{id}) để xóa user. Cấu hình Lambda layers để share common code giữa các functions. Cấu hình environment variables cho table name thay vì hardcode. Test tất cả CRUD operations qua API Gateway | 27/05/2026 | 27/05/2026 | <https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-dynamo-db.html> |
| 5 | Truy cập Step Functions Console. Tạo State Machine để define workflow. Viết ASL (Amazon States Language) definition mô tả các bước trong flow. Thêm Pass state để transform data giữa các bước. Thêm Task state gọi Lambda function để thực hiện business logic. Thêm Choice state cho conditional logic (ví dụ: nếu approved thì làm gì). Thêm Map state để xử lý array items song song. Thêm Parallel state để chạy multiple tasks đồng thời. Execute state machine và kiểm tra execution logs để debug | 28/05/2026 | 28/05/2026 | <https://catalog.workshops.aws/stepfunctions/en-US> |
| 6 | Tạo EventBridge Event Bus riêng để receive custom events. Tạo Rule để bắt EC2 state change events (ví dụ: khi instance start/stop). Cấu hình Target là Lambda function để xử lý khi event match. Tạo API Destination để forward events ra external services. Tạo Scheduler để schedule Lambda invocations theo thời gian. Tạo SQS Queue để nhận và store messages. Tạo Lambda consumer để process SQS messages một cách bất đồng bộ. Cấu hình EventBridge Rule trigger Lambda khi có events. Tạo SNS Topic để gửi notifications. Kết nối tất cả components thành flow hoàn chỉnh để xử lý data pipeline | 29/05/2026 | 29/05/2026 | <https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-get-started.html> |


### Kết quả đạt được tuần 6:

* Tạo và deploy Lambda functions với API Gateway integration.
* Xây dựng Serverless CRUD API với DynamoDB backend.
* Sử dụng Step Functions để orchestrate multi-step workflows.
* Triển khai Event-Driven Architecture với EventBridge và SQS.
