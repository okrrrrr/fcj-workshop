---
title : "Kiểm thử hệ thống"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.3.4. </b> "
---

### Khởi chạy hệ thống

Sau khi hoàn tất việc cấu hình các dịch vụ AWS và triển khai toàn bộ Backend, tiến hành khởi động hệ thống để kiểm tra quá trình hoạt động của kiến trúc Serverless.

Khởi chạy ứng dụng Web và Backend, sau đó truy cập giao diện chính của hệ thống để thực hiện quá trình tải tệp lên.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-20.png)

---

### Thực hiện tải tệp lên hệ thống

Trên giao diện người dùng, lựa chọn một tệp cần kiểm tra và thực hiện tải lên Amazon S3.

Ngay sau khi tệp được tải lên thành công, Amazon S3 sẽ tự động kích hoạt Lambda **S3Handler**, cập nhật trạng thái trong Amazon DynamoDB và gửi yêu cầu xử lý vào Amazon SQS. Tiếp theo, Lambda **Processor** sẽ được kích hoạt và khởi chạy AWS Step Functions để thực hiện quá trình phân tích.

Trong thời gian xử lý, trạng thái của tệp sẽ được hiển thị là **Scanning**.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-21.png)

---

### Kiểm tra kết quả phân tích

Sau khi AWS Step Functions hoàn tất toàn bộ quy trình xử lý, hệ thống sẽ cập nhật trạng thái cuối cùng của tệp.

Nếu tệp không phát hiện mã độc hoặc các dấu hiệu bất thường, kết quả sẽ được hiển thị là **Safe** trên giao diện người dùng.

![](/images/5-Workshop/5.3-Serverless-Backend-Developer/image-22.png)

---

### Theo dõi dữ liệu trên Amazon DynamoDB

Song song với việc hiển thị kết quả trên website, toàn bộ thông tin và trạng thái xử lý của tệp cũng được lưu trữ trong Amazon DynamoDB.

Việc kiểm tra dữ liệu trên DynamoDB giúp xác nhận rằng quá trình đồng bộ giữa Backend và giao diện người dùng diễn ra chính xác. Mỗi khi trạng thái của tệp thay đổi, dữ liệu trong DynamoDB sẽ được cập nhật tương ứng và hiển thị ngay trên website.

---

### Kết quả

Sau khi hoàn thành quá trình kiểm thử, hệ thống hoạt động đúng theo quy trình đã thiết kế:

- Người dùng tải tệp lên giao diện Web.
- Amazon S3 tiếp nhận tệp và kích hoạt Lambda **S3Handler**.
- Lambda **S3Handler** cập nhật trạng thái và gửi yêu cầu vào Amazon SQS.
- Amazon SQS kích hoạt Lambda **Processor** để xử lý.
- AWS Step Functions điều phối toàn bộ quy trình phân tích.
- Kết quả cuối cùng được lưu vào Amazon DynamoDB.
- Website tự động hiển thị trạng thái và kết quả phân tích cho người dùng.

Kết quả kiểm thử cho thấy các dịch vụ AWS đã được tích hợp thành công, quy trình xử lý diễn ra tự động và dữ liệu được đồng bộ chính xác giữa Backend và giao diện người dùng.