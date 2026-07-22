---
title : "Xây dựng AWS CodePipeline"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4.4. </b> "
---

### Tạo AWS CodePipeline

Sau khi hoàn thành việc cấu hình AWS CodeBuild, bước tiếp theo là xây dựng quy trình **Continuous Integration và Continuous Deployment (CI/CD)** bằng dịch vụ **AWS CodePipeline**.

Truy cập dịch vụ **AWS CodePipeline**, chọn **Create pipeline** và lựa chọn hình thức **Build custom pipeline** để tự cấu hình toàn bộ quy trình triển khai.

![](/images/5-Workshop/5.4-Data/image-15.png)

### Cấu hình Pipeline

Tiếp theo, nhập tên Pipeline và cấu hình các thông tin cơ bản như chế độ thực thi (Execution mode) và IAM Service Role để AWS CodePipeline có quyền truy cập các dịch vụ cần thiết trong quá trình triển khai.

![](/images/5-Workshop/5.4-Data/image-16.png)

Sau khi hoàn tất, Pipeline sẽ sử dụng IAM Role này để điều phối toàn bộ quy trình từ lấy mã nguồn, Build cho đến Deploy ứng dụng.

### Kết nối GitHub

Ở bước **Source Stage**, lựa chọn **GitHub (via GitHub App)** làm nguồn mã nguồn của Pipeline.

Sau đó, kết nối tài khoản GitHub, lựa chọn Repository và Branch cần theo dõi. Khi có thay đổi trên Branch được cấu hình, AWS CodePipeline sẽ tự động kích hoạt quy trình Build và Deploy.

![](/images/5-Workshop/5.4-Data/image-17.png)

Tiếp tục kiểm tra lại các thông tin kết nối với GitHub, bao gồm Repository, Branch và định dạng Output Artifact trước khi chuyển sang bước tiếp theo.

![](/images/5-Workshop/5.4-Data/image-18.png)

Việc kết nối GitHub giúp toàn bộ quy trình CI/CD được tự động hóa. Mỗi lần lập trình viên thực hiện **git push**, Pipeline sẽ tự động lấy phiên bản mới nhất của mã nguồn để tiến hành Build và triển khai.

### Cấu hình Build Stage

Sau khi hoàn tất Source Stage, tiến hành cấu hình **Build Stage** bằng cách lựa chọn Project đã tạo trong AWS CodeBuild.

Pipeline sẽ sử dụng Project này để thực hiện các bước được định nghĩa trong tệp **buildspec.yml**, bao gồm cài đặt môi trường, Build ứng dụng và tạo Build Artifact.

![](/images/5-Workshop/5.4-Data/image-19.png)

### Cấu hình Deploy Stage

Bước cuối cùng là cấu hình **Deploy Stage**.

Lựa chọn dịch vụ triển khai là **Amazon S3**, sau đó chỉ định Bucket đích và Build Artifact được tạo từ AWS CodeBuild. Đồng thời bật tùy chọn **Extract file before deploy** để tự động giải nén các tệp trước khi triển khai.

![](/images/5-Workshop/5.4-Data/image-20.png)

Sau khi hoàn tất cấu hình, AWS CodePipeline sẽ tự động thực hiện quy trình:

- Lấy mã nguồn mới nhất từ GitHub.
- Kích hoạt AWS CodeBuild để biên dịch và đóng gói ứng dụng.
- Tạo Build Artifact.
- Triển khai Build Artifact lên Amazon S3.
- Theo dõi trạng thái của từng giai đoạn trong Pipeline.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã xây dựng thành công quy trình **CI/CD** bằng AWS CodePipeline. Từ thời điểm này, mỗi khi mã nguồn trên GitHub được cập nhật, Pipeline sẽ tự động lấy mã nguồn mới, thực hiện Build thông qua AWS CodeBuild và triển khai ứng dụng lên Amazon S3 mà không cần thao tác thủ công. Điều này giúp rút ngắn thời gian triển khai, giảm thiểu sai sót và nâng cao hiệu quả quản lý phiên bản trong quá trình phát triển hệ thống.