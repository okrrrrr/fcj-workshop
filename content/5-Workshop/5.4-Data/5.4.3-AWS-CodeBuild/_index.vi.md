---
title : "Xây dựng AWS CodeBuild"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.4.3. </b> "
---

### Tạo dự án AWS CodeBuild

Sau khi mã nguồn đã được đưa lên GitHub và hoàn tất cấu hình tệp **buildspec.yml**, bước tiếp theo là tạo một dự án trên **AWS CodeBuild** để tự động biên dịch và đóng gói ứng dụng.

Truy cập dịch vụ **AWS CodeBuild**, chọn **Create build project** và nhập các thông tin cơ bản như tên Project, nguồn mã nguồn (Source Provider) và Repository GitHub cần sử dụng.

![](/images/5-Workshop/5.4-Data/image-12.png)

### Cấu hình môi trường Build

Tiếp theo, cấu hình môi trường thực thi cho AWS CodeBuild. Trong phần này, lựa chọn hệ điều hành **Amazon Linux**, Runtime phù hợp với ứng dụng và Image do AWS cung cấp.

Ngoài ra, lựa chọn chế độ **On-demand** để CodeBuild tự động khởi tạo môi trường khi có yêu cầu Build, giúp tối ưu chi phí sử dụng.

![](/images/5-Workshop/5.4-Data/image-13.png)

Các thông số chính được cấu hình bao gồm:

- **Provisioning model:** On-demand.
- **Environment image:** Managed image.
- **Compute:** EC2.
- **Running mode:** Container.
- **Operating System:** Amazon Linux.
- **Runtime:** Standard.
- **Image:** AWS CodeBuild Managed Image.

Sau khi hoàn tất cấu hình môi trường, AWS CodeBuild sẽ sử dụng các thông số này để tạo môi trường Build mỗi khi Pipeline được kích hoạt.

### Khởi chạy dự án CodeBuild

Sau khi hoàn thành việc cấu hình, tiến hành tạo Project và kiểm tra trạng thái hoạt động của AWS CodeBuild.

![](/images/5-Workshop/5.4-Data/image-14.png)

Tại giao diện Project, người dùng có thể theo dõi các thông tin như:

- Trạng thái của lần Build gần nhất.
- Repository đang được liên kết.
- Vị trí lưu trữ Build Artifact.
- Nhật ký (Logs) của quá trình Build.
- Lịch sử các lần thực thi Build.

Việc theo dõi các thông tin này giúp nhanh chóng phát hiện lỗi và đánh giá kết quả của quá trình Build trước khi chuyển sang bước triển khai tự động bằng AWS CodePipeline.

### Hoàn thành

Sau khi hoàn tất các bước trên, dự án **AWS CodeBuild** đã được tạo và cấu hình thành công. Hệ thống đã sẵn sàng tự động lấy mã nguồn từ GitHub, thực hiện quá trình Build theo tệp **buildspec.yml** và tạo ra các Artifact phục vụ cho quá trình triển khai trong AWS CodePipeline.