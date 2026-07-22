---
title : "Cấu hình Amazon SQS và AWS Lambda"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.3.2. </b> "
---

### Tạo Amazon SQS

Sau khi hoàn tất việc chuẩn bị mã nguồn Backend và cơ sở dữ liệu DynamoDB, bước tiếp theo là tạo **Amazon Simple Queue Service (Amazon SQS)**. Dịch vụ này đóng vai trò là hàng đợi trung gian giúp lưu trữ các yêu cầu xử lý, đảm bảo hệ thống hoạt động ổn định ngay cả khi có nhiều người dùng tải tệp lên cùng lúc.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-6.png)

Sau khi Queue được tạo thành công, sao chép **Queue URL** và lưu lại để sử dụng trong quá trình cấu hình các Lambda Function.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-7.png)

Tiếp tục đặt tên cho Queue và hoàn tất quá trình tạo.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-8.png)

Trong hệ thống sử dụng hai loại Queue:

- **Main Queue**: Chứa các yêu cầu xử lý được gửi từ Amazon S3 sau khi người dùng tải tệp lên.
- **Dead Letter Queue (DLQ)**: Lưu trữ các yêu cầu bị lỗi sau nhiều lần xử lý không thành công, giúp dễ dàng theo dõi và khắc phục sự cố.

Việc sử dụng SQS giúp các thành phần trong hệ thống giao tiếp với nhau theo cơ chế bất đồng bộ (Asynchronous), tăng khả năng mở rộng và giảm tải cho các dịch vụ xử lý.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-9.png)

### Tạo IAM Role cho AWS Lambda

Để các Lambda Function có thể truy cập các dịch vụ AWS như Amazon S3, DynamoDB, Amazon SQS và Step Functions, cần tạo một **IAM Role** và cấp đầy đủ các quyền cần thiết.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-10.png)

Sau khi IAM Role được tạo, tiến hành tạo các **AWS Lambda Function** và tải các tệp **.zip** đã chuẩn bị ở phần trước lên từng Function tương ứng.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-11.png)

### Cấu hình Amazon S3 Trigger

Tiếp theo, cấu hình **Amazon S3 Event Notification** để mỗi khi người dùng tải tệp lên Bucket, Amazon S3 sẽ tự động kích hoạt Lambda **S3Handler**.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-12.png)

Lambda **S3Handler** sẽ thực hiện các nhiệm vụ sau:

- Nhận thông tin tệp vừa được tải lên Amazon S3.
- Cập nhật trạng thái của tệp trong Amazon DynamoDB thành **received**.
- Gửi một thông điệp (Message) vào Amazon SQS để tiếp tục xử lý.

### Cấu hình Amazon SQS Trigger

Sau khi thông điệp được gửi vào hàng đợi Amazon SQS, cấu hình Trigger để mỗi Message mới sẽ tự động kích hoạt Lambda **Processor**.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-13.png)

Lambda **Processor** sẽ thực hiện các công việc sau:

- Đọc Message từ Amazon SQS.
- Cập nhật trạng thái của tệp trong DynamoDB thành **scanning**.
- Khởi chạy quy trình xử lý thông qua AWS Step Functions.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-14.png)

Sau khi hoàn tất cấu hình Trigger, tiến hành kiểm tra lại toàn bộ các Lambda Function để đảm bảo các Trigger đã được liên kết chính xác.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-15.png)

### Cập nhật tệp cấu hình môi trường

Cuối cùng, cập nhật tệp **.env** với các thông tin như Queue URL, tên DynamoDB Table, tên S3 Bucket và các ARN cần thiết để các Lambda Function có thể giao tiếp chính xác với các dịch vụ AWS.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã cấu hình thành công Amazon SQS và AWS Lambda. Từ thời điểm này, mỗi khi người dùng tải tệp lên Amazon S3, hệ thống sẽ tự động tiếp nhận yêu cầu, cập nhật trạng thái xử lý và chuyển sang bước điều phối quy trình bằng AWS Step Functions.