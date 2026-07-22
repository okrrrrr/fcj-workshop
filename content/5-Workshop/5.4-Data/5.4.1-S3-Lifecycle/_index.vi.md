---
title : "Cấu hình Amazon S3 và Lifecycle Rule"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.4.1. </b> "
---

### Tạo Amazon S3 Bucket

Sau khi hoàn thành việc xây dựng Frontend và Serverless Backend, bước tiếp theo là cấu hình dịch vụ lưu trữ **Amazon Simple Storage Service (Amazon S3)**. Đây là nơi lưu trữ các tệp do người dùng tải lên để phục vụ quá trình phân tích của hệ thống.

Truy cập dịch vụ **Amazon S3**, chọn **Create bucket** và nhập các thông tin cần thiết như tên Bucket, Region và các thiết lập ban đầu.

![](/images/5-Workshop/5.4-Data/image.png)

### Cấu hình Bucket

Tiếp theo, cấu hình các thiết lập cho Bucket như chế độ lưu trữ, khả năng mở rộng và phương thức quản lý dữ liệu. Việc lựa chọn cấu hình phù hợp sẽ giúp hệ thống đáp ứng tốt nhu cầu lưu trữ và truy cập dữ liệu.

![](/images/5-Workshop/5.4-Data/image-1.png)

Sau đó, tiếp tục cấu hình các tùy chọn về sao lưu, phiên bản dữ liệu (Versioning) và các thiết lập bổ sung trước khi hoàn tất việc tạo Bucket.

![](/images/5-Workshop/5.4-Data/image-2.png)

Sau khi kiểm tra lại toàn bộ thông tin cấu hình, chọn **Create bucket** để hoàn tất quá trình tạo Amazon S3 Bucket.

![](/images/5-Workshop/5.4-Data/image-3.png)

### Cấu hình Lifecycle Rule

Sau khi Bucket được tạo thành công, chuyển sang tab **Management** và chọn **Create lifecycle rule** để thiết lập quy tắc quản lý vòng đời của các đối tượng lưu trữ trong Bucket.

![](/images/5-Workshop/5.4-Data/image-4.png)

Nhập tên cho Lifecycle Rule, lựa chọn phạm vi áp dụng và cấu hình các điều kiện chuyển đổi hoặc xóa đối tượng theo thời gian sử dụng.

![](/images/5-Workshop/5.4-Data/image-5.png)

Tiếp theo, xem lại các thiết lập của Lifecycle Rule trước khi áp dụng cho Bucket.

![](/images/5-Workshop/5.4-Data/image-6.png)

Sau khi hoàn tất, Lifecycle Rule sẽ xuất hiện trong danh sách quản lý của Bucket và được tự động áp dụng cho các đối tượng lưu trữ theo các điều kiện đã cấu hình.

![](/images/5-Workshop/5.4-Data/image-7.png)

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã tạo thành công **Amazon S3 Bucket** để lưu trữ dữ liệu và cấu hình **Lifecycle Rule** nhằm tự động quản lý vòng đời của các tệp. Việc áp dụng Lifecycle Rule giúp tối ưu chi phí lưu trữ, tự động xử lý các tệp không còn sử dụng và nâng cao hiệu quả quản lý dữ liệu trong hệ thống.

![](/images/5-Workshop/5.4-Data/image-8.png)