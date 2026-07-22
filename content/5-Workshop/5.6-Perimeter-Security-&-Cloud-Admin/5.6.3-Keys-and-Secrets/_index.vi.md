---
title : "Quản lý khóa mã hóa và thông tin bí mật"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.6.3. </b> "
---

### Tạo Secret trong AWS Secrets Manager

Sau khi hoàn tất việc cấu hình AWS WAF, bước tiếp theo là triển khai **AWS Secrets Manager** để quản lý tập trung các thông tin nhạy cảm của hệ thống.

Truy cập dịch vụ **AWS Secrets Manager**, chọn **Store a new secret** và tiến hành tạo một Secret mới.

![](/fcj-workshop/images/5-Workshop/5.6-Perimeter-Security-&-Cloud-Admin/image-8.png)

Trong Secret, lưu trữ các thông tin quan trọng như:

- API Key.
- Mật khẩu cơ sở dữ liệu (Database Password).
- Các thông tin xác thực khác được sử dụng trong quá trình triển khai và vận hành hệ thống.

Việc sử dụng AWS Secrets Manager giúp các ứng dụng truy cập thông tin nhạy cảm một cách an toàn mà không cần lưu trực tiếp trong mã nguồn hoặc tệp cấu hình.

### Tạo Customer Managed Key với AWS KMS

Sau khi tạo Secret, tiếp tục cấu hình **AWS Key Management Service (AWS KMS)** để quản lý khóa mã hóa phục vụ cho việc bảo vệ dữ liệu của hệ thống.

Tạo một **Customer Managed Key (CMK)** với tên **kms-project-key**.

![](/fcj-workshop/images/5-Workshop/5.6-Perimeter-Security-&-Cloud-Admin/image-9.png)

Khóa mã hóa này được sử dụng để:

- Mã hóa dữ liệu lưu trữ trên các dịch vụ AWS.
- Bảo vệ các Secret được lưu trong AWS Secrets Manager.
- Hỗ trợ các dịch vụ AWS khác khi cần mã hóa hoặc giải mã dữ liệu.
- Đảm bảo chỉ những tài nguyên và người dùng được cấp quyền mới có thể sử dụng khóa mã hóa.

### Vai trò của Secrets Manager và AWS KMS

Kết hợp AWS Secrets Manager và AWS KMS mang lại nhiều lợi ích trong việc bảo mật hệ thống, bao gồm:

- Quản lý tập trung các thông tin nhạy cảm.
- Giảm nguy cơ lộ API Key hoặc mật khẩu trong mã nguồn.
- Mã hóa dữ liệu bằng khóa do tổ chức quản lý.
- Hỗ trợ kiểm soát quyền truy cập theo chính sách IAM.
- Đáp ứng các yêu cầu về bảo mật và quản lý dữ liệu trên môi trường Cloud.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã cấu hình thành công **AWS Secrets Manager** để lưu trữ thông tin bí mật và **AWS KMS** để quản lý khóa mã hóa. Việc kết hợp hai dịch vụ này giúp nâng cao khả năng bảo vệ dữ liệu, giảm thiểu rủi ro rò rỉ thông tin và tăng cường mức độ an toàn cho toàn bộ hệ thống.