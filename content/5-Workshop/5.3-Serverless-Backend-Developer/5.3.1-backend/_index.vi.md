---
title : "Chuẩn bị mã nguồn Backend và tạo DynamoDB"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.3.1. </b> "
---

### Chuẩn bị mã nguồn Backend

Đầu tiên, tiến hành chuẩn bị mã nguồn Backend của hệ thống. Backend được xây dựng theo mô hình Serverless, trong đó mỗi chức năng được triển khai dưới dạng một AWS Lambda Function để xử lý các nghiệp vụ như tiếp nhận tệp, phân tích dữ liệu, cập nhật trạng thái và gửi thông báo.

Mã nguồn được chia thành **08 Lambda Functions**, mỗi hàm đảm nhận một chức năng riêng nhằm giúp hệ thống dễ quản lý, mở rộng và bảo trì.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image.png)

### Chuẩn bị source Backend

Sau khi hoàn thành mã nguồn, truy cập vào thư mục Backend đã được xây dựng trước đó để tiến hành đóng gói và triển khai lên AWS Lambda.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-1.png)

### Đóng gói các Lambda Function

Tiếp theo, thực hiện đóng gói toàn bộ các Lambda Function thành các tệp **.zip**. Việc đóng gói giúp AWS Lambda có thể tiếp nhận và triển khai từng chức năng một cách độc lập.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-2.png)

Sau khi chạy script, hệ thống sẽ tự động tạo các tệp nén cho từng Lambda Function.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-3.png)

Mỗi tệp **.zip** bao gồm:

- File `app.js`.
- File `package.json`.
- Thư mục `node_modules`.

Các tệp sau khi đóng gói sẽ được sử dụng để tải lên dịch vụ AWS Lambda trong các bước tiếp theo.

### Tạo Amazon DynamoDB

Sau khi chuẩn bị mã nguồn Backend, tiến hành tạo cơ sở dữ liệu **Amazon DynamoDB** để lưu trữ thông tin và trạng thái xử lý của các tệp được tải lên hệ thống.

Tại giao diện DynamoDB, chọn **Create table**, nhập tên bảng và cấu hình các thông số cần thiết trước khi tạo bảng.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-4.png)

### Tạo Global Secondary Index

Sau khi bảng được tạo thành công, chuyển sang tab **Indexes** và tạo thêm một **Global Secondary Index (GSI)** với tên **userID-index**.

Index này được sử dụng để tìm kiếm và truy vấn dữ liệu theo **User ID**, giúp tăng hiệu năng truy xuất dữ liệu trong quá trình xử lý và hiển thị kết quả.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-5.png)

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã chuẩn bị xong mã nguồn Backend, đóng gói các Lambda Function và xây dựng cơ sở dữ liệu Amazon DynamoDB phục vụ cho quá trình triển khai các dịch vụ Serverless trong những phần tiếp theo.