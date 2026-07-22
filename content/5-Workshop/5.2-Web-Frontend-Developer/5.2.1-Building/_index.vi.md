---
title : "Xây dựng Frontend React và Amazon Cognito"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.2.1 </b> "
---

### Cấu trúc thư mục Frontend React và AWS SDK

Đầu tiên, tiến hành xây dựng và tổ chức cấu trúc thư mục của ứng dụng Frontend bằng React. Việc phân chia các thư mục theo từng chức năng giúp mã nguồn dễ quản lý, bảo trì và mở rộng trong quá trình phát triển.

Ứng dụng Frontend sử dụng AWS SDK để kết nối và tương tác với các dịch vụ AWS như Amazon Cognito, Amazon S3 và Cognito Identity Pool.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image.png)

### Tạo file AWS.ts để cấu hình AWS Services

Trong thư mục dự án, tạo file `AWS.ts` để lưu trữ các thông tin cấu hình cần thiết cho việc kết nối giữa ứng dụng React và các dịch vụ AWS.

Các thông tin cấu hình thường bao gồm:

* AWS Region.
* User Pool ID.
* App Client ID.
* Identity Pool ID.
* Tên S3 Bucket.

Việc quản lý cấu hình trong một file riêng giúp thuận tiện khi cập nhật thông tin và hạn chế việc khai báo lặp lại trong nhiều thành phần của ứng dụng.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-1.png)

### Truy cập AWS Management Console

Truy cập AWS Management Console và đăng nhập bằng tài khoản AWS được cấp để bắt đầu quá trình cấu hình các dịch vụ phục vụ cho ứng dụng Frontend.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-2.png)

### Tìm kiếm dịch vụ Amazon Cognito

Tại giao diện AWS Management Console, nhập từ khóa `Cognito` vào thanh tìm kiếm.

Chọn dịch vụ **Amazon Cognito** trong danh sách kết quả để truy cập trang quản lý xác thực người dùng.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-3.png)

### Tạo User Pool mới

Tại trang quản lý Amazon Cognito, chọn chức năng **Create user pool** để bắt đầu tạo một User Pool mới.

User Pool được sử dụng để quản lý thông tin đăng ký, đăng nhập và xác thực người dùng cho ứng dụng React.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-4.png)

### Cấu hình User Directory

Tại bước tạo User Pool, thực hiện các cấu hình sau:

* Chọn loại ứng dụng **Single-page application (SPA)**.
* Tại mục **Name your application**, nhập tên ứng dụng.
* Chọn **Email** làm phương thức đăng nhập.
* Tick chọn **Enable self-registration** để cho phép người dùng tự đăng ký tài khoản.
* Mở danh sách **Select attributes**.
* Tìm và chọn thuộc tính **Name**.
* Kiểm tra lại các thông tin đã cấu hình.
* Chọn chức năng tạo User Pool để hoàn tất.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-5.png)

### Lưu User Pool ID

Sau khi User Pool được tạo thành công, hệ thống chuyển đến trang tổng quan của User Pool.

Tại trang **Overview**, sao chép và lưu lại giá trị **User Pool ID**. Thông tin này sẽ được sử dụng trong file `AWS.ts` để kết nối ứng dụng React với Amazon Cognito.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-6.png)

### Lấy App Client ID

Trong giao diện quản lý User Pool, thực hiện các bước sau:

* Chọn mục **Applications**.
* Chọn **App clients**.
* Tìm App Client đã được tạo cùng với User Pool.
* Sao chép và lưu lại giá trị **Client ID**.
* Nhấn vào tên App Client để xem thông tin chi tiết.

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-7.png)

![](/images/5-Workshop/5.2-Web-Frontend-Developer/image-8.png)

### Chỉnh sửa App Client

Trong trang thông tin chi tiết của App Client, chọn **Edit** để kiểm tra hoặc cập nhật các thiết lập liên quan đến ứng dụng React.

Sau khi hoàn tất, lưu lại các thay đổi và cập nhật giá trị **User Pool ID** cùng **Client ID** vào file `AWS.ts`.
