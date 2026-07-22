---
title : "Cấu hình AWS WAF bảo vệ API Gateway"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.6.2. </b> "
---

### Tạo Web ACL

Sau khi hoàn tất việc cấu hình IAM OIDC Provider và GitHub Actions, bước tiếp theo là triển khai **AWS Web Application Firewall (AWS WAF)** nhằm tăng cường khả năng bảo vệ hệ thống trước các cuộc tấn công từ Internet.

Truy cập dịch vụ **AWS WAF & Shield**, chọn **Create web ACL** để khởi tạo một **Web Access Control List (Web ACL)** mới. Web ACL sẽ được sử dụng để kiểm soát và lọc các yêu cầu gửi đến **Amazon API Gateway**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-5.png)

### Hoàn tất tạo Web ACL

Sau khi cấu hình các thông tin cần thiết như tên, Region và tài nguyên cần bảo vệ, tiến hành tạo Web ACL.

![](/images/5-Workshop/5.6-Perimeter-Security/image-6.png)

Sau khi được tạo thành công, Web ACL sẽ được liên kết với API Gateway để kiểm tra và đánh giá tất cả các yêu cầu truy cập trước khi chuyển đến Backend.

### Cấu hình Rate-based Rule

Tiếp theo, tạo một **Rate-based Rule** nhằm giới hạn số lượng yêu cầu mà một địa chỉ IP có thể gửi đến API Gateway trong một khoảng thời gian nhất định.

![](/images/5-Workshop/5.6-Perimeter-Security/image-7.png)

Trong cấu hình này, thiết lập hành động **Block** đối với các địa chỉ IP gửi quá **100 yêu cầu trong vòng 5 phút**. Quy tắc này giúp hạn chế các hành vi gửi yêu cầu với tần suất cao bất thường, góp phần giảm thiểu nguy cơ tấn công từ chối dịch vụ (DoS) hoặc Spam API.

### Vai trò của AWS WAF

Sau khi được cấu hình, AWS WAF sẽ thực hiện các nhiệm vụ sau:

- Kiểm tra các yêu cầu gửi đến Amazon API Gateway.
- Tự động chặn các địa chỉ IP vượt quá ngưỡng truy cập đã cấu hình.
- Giảm thiểu nguy cơ tấn công DoS và Spam API.
- Bảo vệ hệ thống trước các lưu lượng truy cập bất thường.
- Tăng cường lớp bảo mật ở tầng ứng dụng trước khi yêu cầu được chuyển đến Backend.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã triển khai thành công **AWS WAF** để bảo vệ Amazon API Gateway. Web ACL kết hợp với **Rate-based Rule** giúp giám sát lưu lượng truy cập, tự động chặn các yêu cầu vượt quá giới hạn cho phép và góp phần nâng cao mức độ an toàn cho toàn bộ hệ thống.