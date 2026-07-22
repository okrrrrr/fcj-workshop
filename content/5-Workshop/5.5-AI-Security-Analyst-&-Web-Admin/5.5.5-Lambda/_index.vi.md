---
title : "Cấu hình AWS Lambda"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5.5 </b> "
---

### Giới thiệu

- Trong phần này, bạn sẽ tạo và cấu hình một AWS Lambda Function để xử lý các yêu cầu phân tích URL từ Amazon API Gateway. Lambda sẽ đóng vai trò trung gian giữa API Gateway và Bastion Host, gửi yêu cầu đến Nginx Reverse Proxy đang chạy trên Bastion Host và nhận kết quả phân tích từ Flask API trên Private EC2 trước khi trả kết quả về cho người dùng.

### Tạo Lambda Function

+ Cấu hình Lambda:
    + Function name: url-analyzer-lambda
    + Runtime: Node.js 22.x
    + Architecture: x86_64
    + Execution role: Create a new role with basic Lambda permissions

![alt text](image.png)

### Cấu hình biến môi trường

- Chọn **Configuration → Environment variables → Edit.**

![alt text](image-1.png)

### Cập nhật mã nguồn Lambda 

- Sau khi cập nhật mã nguồn chọn **deloy**

![alt text](image-2.png)

- Lambda Function đã triển khai thành công

### Kiểm tra Lambda Function

- Chọn test rồi tạo test event

```
{
  "body": "{\"url\":\"https://google.com\"}"
}
```

![alt text](image-3.png)

- Lambda Function đã test thành công biết phân biết được đường dẫn url là an toàn hay độc hại.

