---
title : "Cấu hình S3, Identity Pool và IAM Role"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.2.2. </b> "
-------------------------

### Tạo Amazon S3 Bucket

Truy cập dịch vụ **Amazon S3** trên AWS Management Console.

Tại trang quản lý S3, chọn **Create bucket** để bắt đầu tạo một Bucket mới dùng để lưu trữ các file của ứng dụng.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-9.png)

### Cấu hình thông tin S3 Bucket

Tại trang tạo Bucket, thực hiện các bước sau:

* Nhập tên Bucket tại mục **Bucket name**.
* Chọn AWS Region phù hợp với hệ thống.
* Giữ nguyên hoặc điều chỉnh các thiết lập khác theo yêu cầu.
* Kéo xuống cuối trang.
* Chọn **Create bucket** để hoàn tất.

Tên Bucket phải là duy nhất trên toàn bộ hệ thống Amazon S3.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-10.png)


### Cấu hình CORS cho S3 Bucket

Sau khi tạo Bucket thành công, chọn Bucket vừa tạo và thực hiện các bước sau:

* Chọn tab **Permissions**.
* Kéo xuống phần **Cross-origin resource sharing (CORS)**.
* Chọn **Edit**.
* Nhập cấu hình CORS cho phép ứng dụng React truy cập S3 Bucket.
* Chọn **Save changes** để lưu cấu hình.

Việc cấu hình CORS giúp trình duyệt cho phép ứng dụng Frontend gửi yêu cầu đến Amazon S3 từ một tên miền hoặc cổng khác.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-11.png)


### Tạo Cognito Identity Pool

Quay lại dịch vụ Amazon Cognito và truy cập chức năng quản lý **Identity pools**.

Chọn chức năng tạo Identity Pool mới để cấp quyền truy cập tài nguyên AWS cho người dùng sau khi đăng nhập.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-12.png)


### Cấu hình quyền truy cập cho Identity Pool

Tại bước cấu hình Identity Pool, thực hiện các thao tác sau:

* Tick chọn **Authenticated access**.
* Chọn **Amazon Cognito user pool** làm nguồn xác thực.
* Chọn **Next** để tiếp tục.
* Chọn **User Pool ID** đã tạo ở phần trước.
* Chọn **App Client ID** tương ứng.
* Giữ nguyên các lựa chọn khác nếu không có yêu cầu thay đổi.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-13.png)


### Cấu hình IAM Role cho Identity Pool

Sau khi liên kết User Pool và App Client, chọn **Next** để chuyển sang bước cấu hình quyền truy cập.

Tại bước này, AWS sẽ tạo hoặc cho phép lựa chọn IAM Role dành cho người dùng đã xác thực.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-14.png)


### Đặt tên Identity Pool

Tại mục **Identity pool name**, nhập tên cho Identity Pool.

Sau đó:

* Kiểm tra thông tin đã cấu hình.
* Chọn **Next** để tiếp tục.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-15.png)


### Kiểm tra và tạo Identity Pool

Tại trang xác nhận, kiểm tra lại các thông tin gồm:

* Tên Identity Pool.
* Loại quyền truy cập.
* User Pool ID.
* App Client ID.
* IAM Role được liên kết.

Nếu các thông tin đã chính xác, chọn chức năng tạo Identity Pool.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-16.png)


Sau khi tạo thành công, sao chép và lưu lại giá trị **Identity Pool ID** để cập nhật vào file `AWS.ts`.

### Truy cập Amazon IAM

Truy cập dịch vụ **Identity and Access Management (IAM)** trên AWS Management Console.

Trong giao diện IAM, chọn mục **Roles** để xem danh sách các Role hiện có.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-17.png)


### Chọn IAM Role của Identity Pool

Tìm IAM Role được AWS tạo cho người dùng đã xác thực của Cognito Identity Pool.

Tên Role thường chứa tên Identity Pool và cụm từ liên quan đến người dùng đã xác thực.

Chọn Role để xem và cấu hình quyền.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-18.png)


![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-19.png)


### Thêm quyền truy cập Amazon S3

Trong trang chi tiết IAM Role, thực hiện các bước sau:

* Chọn tab **Permissions**.
* Chọn **Add permissions**.
* Chọn **Attach policies**.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-20.png)


### Gắn chính sách AmazonS3FullAccess

Tại ô tìm kiếm Policy, nhập:

```text
AmazonS3FullAccess
```

Sau đó thực hiện:

* Tick chọn Policy **AmazonS3FullAccess**.
* Chọn **Attach policies** để gắn quyền vào IAM Role.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-21.png)


### Kiểm tra cấu hình

Sau khi hoàn tất, kiểm tra lại các thông tin cấu hình trong file `AWS.ts`, bao gồm:

* AWS Region.
* User Pool ID.
* App Client ID.
* Identity Pool ID.
* Tên S3 Bucket.

Tiếp theo, chạy ứng dụng React và kiểm tra khả năng:

* Đăng ký tài khoản.
* Đăng nhập người dùng.
* Xác thực thông qua Amazon Cognito.
* Nhận quyền truy cập từ Identity Pool.
* Kết nối và thao tác với Amazon S3.

Kết quả kiểm tra giúp xác nhận ứng dụng Frontend đã được kết nối đúng với các dịch vụ AWS.
