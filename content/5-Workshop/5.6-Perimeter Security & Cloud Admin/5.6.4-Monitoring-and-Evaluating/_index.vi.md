---
title : "Giám sát và đánh giá tuân thủ hệ thống"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.6.4. </b> "
---

### Cấu hình AWS CloudTrail

Sau khi hoàn tất việc cấu hình các cơ chế bảo mật, bước tiếp theo là triển khai **AWS CloudTrail** để ghi nhận toàn bộ các hoạt động diễn ra trên tài khoản AWS.

Truy cập dịch vụ **AWS CloudTrail**, chọn **Create trail** và tiến hành tạo một Trail mới với tên **main-project-trail**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-10.png)

CloudTrail sẽ tự động ghi nhận các thao tác quản trị, thay đổi cấu hình và các sự kiện phát sinh trên các dịch vụ AWS. Toàn bộ nhật ký (Audit Logs) sẽ được lưu trữ trong Amazon S3 để phục vụ việc theo dõi, kiểm tra và phân tích khi cần thiết.

### Cấu hình AWS Config

Tiếp theo, triển khai **AWS Config** nhằm theo dõi liên tục trạng thái cấu hình của các tài nguyên trong hệ thống.

Tại giao diện AWS Config, tiến hành cấu hình **Configuration Recorder** để ghi nhận mọi thay đổi về cấu hình của các dịch vụ AWS.

![](/images/5-Workshop/5.6-Perimeter-Security/image-11.png)

Sau khi Configuration Recorder được kích hoạt, AWS Config sẽ tự động theo dõi các thay đổi của tài nguyên và đánh giá mức độ tuân thủ dựa trên các Rule đã được thiết lập.

### Kiểm tra Compliance Rule

Sau khi hoàn tất cấu hình, kiểm tra kết quả đánh giá của các Rule trong AWS Config.

Trong hệ thống, Rule **s3-bucket-public-read-prohibited** được sử dụng để kiểm tra việc ngăn chặn truy cập công khai đối với các Amazon S3 Bucket.

![](/images/5-Workshop/5.6-Perimeter-Security/image-12.png)

Kết quả hiển thị trạng thái **Compliant**, cho thấy các S3 Bucket đã đáp ứng yêu cầu bảo mật và không cho phép truy cập đọc công khai trái phép.

### Theo dõi Dashboard của AWS Config

Cuối cùng, truy cập **AWS Config Dashboard** để theo dõi tổng quan tình trạng tuân thủ của toàn bộ tài nguyên trong hệ thống.

![](/images/5-Workshop/5.6-Perimeter-Security/image-13.png)

Dashboard cung cấp các thông tin như:

- Số lượng tài nguyên đang được AWS Config theo dõi.
- Kết quả đánh giá Compliance của từng Rule.
- Trạng thái tuân thủ của các Amazon S3 Bucket.
- Thống kê các tài nguyên đạt hoặc chưa đạt yêu cầu bảo mật.
- Báo cáo tổng quan giúp quản trị viên dễ dàng giám sát hệ thống.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã triển khai thành công **AWS CloudTrail** và **AWS Config** để giám sát hoạt động cũng như đánh giá mức độ tuân thủ của các tài nguyên AWS. CloudTrail hỗ trợ ghi nhận đầy đủ các nhật ký quản trị, trong khi AWS Config theo dõi liên tục trạng thái cấu hình và kiểm tra việc tuân thủ các chính sách bảo mật. Nhờ đó, quản trị viên có thể nhanh chóng phát hiện các thay đổi, kiểm tra lịch sử hoạt động và duy trì môi trường Cloud an toàn, ổn định.