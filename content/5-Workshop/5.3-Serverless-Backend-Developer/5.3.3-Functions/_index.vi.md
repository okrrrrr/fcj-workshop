---
title : "Xây dựng AWS Step Functions"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3. </b> "
---

### Tạo IAM Role cho AWS Step Functions

Sau khi hoàn tất cấu hình Amazon SQS và các AWS Lambda Function, bước tiếp theo là tạo **IAM Role** dành cho **AWS Step Functions**. IAM Role này sẽ cấp quyền để Step Functions có thể gọi các Lambda Function và truy cập vào Amazon DynamoDB trong quá trình điều phối workflow.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-16.png)

IAM Role được cấp các quyền cần thiết như:

- Thực thi các AWS Lambda Function.
- Đọc và ghi dữ liệu trên Amazon DynamoDB.
- Ghi nhật ký hoạt động vào Amazon CloudWatch Logs.

Sau khi hoàn thành, IAM Role sẽ được gán cho State Machine trong AWS Step Functions.

---

### Tạo AWS Step Functions

Tiếp theo, truy cập dịch vụ **AWS Step Functions** và tạo một **State Machine** mới để điều phối toàn bộ quy trình xử lý tệp.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-17.png)

Sau khi tạo State Machine, tiến hành cấu hình các trạng thái (States) và liên kết với các Lambda Function tương ứng.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-18.png)

Workflow của hệ thống bao gồm các bước chính:

- **Validate:** Kiểm tra thông tin và trạng thái của tệp được tải lên.
- **Analyze:** Thực hiện quá trình phân tích và kiểm tra tệp.
- **Notify:** Cập nhật kết quả cuối cùng và thông báo cho người dùng.

Mỗi bước trong workflow sẽ gọi một Lambda Function riêng biệt, giúp quá trình xử lý được tách biệt, dễ quản lý và dễ mở rộng.

---

### Cập nhật ARN cho các Lambda Function

Sau khi State Machine được tạo thành công, sao chép **ARN (Amazon Resource Name)** của State Machine và cập nhật vào biến môi trường của các Lambda Function sau:

- `malware-analysis-update-dev`
- `malware-analysis-s3-handler-dev`
- `malware-analysis-processor-dev`

Việc cấu hình ARN giúp các Lambda Function có thể khởi chạy State Machine mỗi khi có yêu cầu xử lý mới.

---

### Kiểm tra Workflow

Sau khi hoàn tất cấu hình, tiến hành kiểm tra lại toàn bộ Workflow trong AWS Step Functions để đảm bảo các trạng thái đã được liên kết đúng và có thể thực hiện theo đúng thứ tự.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-19.png)

Workflow sẽ hoạt động theo trình tự sau:

1. Người dùng tải tệp lên Amazon S3.
2. Amazon S3 kích hoạt Lambda **S3Handler**.
3. Lambda **S3Handler** cập nhật trạng thái và gửi Message vào Amazon SQS.
4. Amazon SQS kích hoạt Lambda **Processor**.
5. Lambda **Processor** khởi chạy AWS Step Functions.
6. AWS Step Functions lần lượt thực hiện các bước **Validate → Analyze → Notify**.
7. Kết quả cuối cùng được cập nhật vào Amazon DynamoDB để hiển thị trên giao diện người dùng.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã xây dựng thành công quy trình điều phối bằng **AWS Step Functions**. Toàn bộ quá trình xử lý được tự động hóa, giúp các Lambda Function phối hợp với nhau theo đúng trình tự, giảm sự phụ thuộc giữa các thành phần và tăng khả năng mở rộng của hệ thống.