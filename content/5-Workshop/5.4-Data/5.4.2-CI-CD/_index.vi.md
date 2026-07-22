---
title : "Chuẩn bị môi trường CI/CD"
date : 2024-01-01
weight : 2
chapter : false
pre : " <b> 5.4.2. </b> "
---

### Xây dựng tệp buildspec.yml

Sau khi hoàn tất việc cấu hình Amazon S3 và Lifecycle Rule, bước tiếp theo là chuẩn bị môi trường **Continuous Integration/Continuous Deployment (CI/CD)**. Trong AWS CodeBuild, tệp **buildspec.yml** đóng vai trò mô tả toàn bộ các bước mà hệ thống sẽ thực hiện trong quá trình Build và Deploy.

Tạo tệp **buildspec.yml** tại thư mục gốc của dự án và cấu hình các biến môi trường, phiên bản Runtime cũng như các giai đoạn xử lý.

![](/images/5-Workshop/5.4-Data/image-9.png)

Trong tệp **buildspec.yml**, quy trình Build được chia thành các giai đoạn chính:

- **Install:** Cài đặt các thư viện và môi trường cần thiết cho quá trình Build.
- **Pre-build:** Kiểm tra phiên bản của các công cụ và chuẩn bị môi trường thực thi.
- **Build:** Biên dịch và đóng gói ứng dụng Backend bằng AWS SAM.
- **Post-build:** Đóng gói (Package) và triển khai (Deploy) ứng dụng lên AWS.

### Cấu hình quá trình Deploy

Sau khi hoàn tất các bước Build, tiếp tục cấu hình giai đoạn **Post-build** trong tệp **buildspec.yml**.

Giai đoạn này sẽ thực hiện các tác vụ như:

- Đóng gói ứng dụng bằng AWS SAM.
- Tạo tệp `packaged.yaml`.
- Tải các Artifact lên Amazon S3.
- Triển khai Stack lên AWS CloudFormation.
- Lưu trữ các Artifact phục vụ cho các bước tiếp theo trong quy trình CI/CD.

![](/images/5-Workshop/5.4-Data/image-10.png)

### Đưa mã nguồn lên GitHub

Sau khi hoàn thiện tệp **buildspec.yml**, tiến hành lưu các thay đổi của dự án và đồng bộ mã nguồn lên GitHub.

Thực hiện Commit các thay đổi và sử dụng lệnh **git push** để cập nhật Repository từ máy phát triển lên GitHub.

![](/images/5-Workshop/5.4-Data/image-11.png)

Việc lưu trữ mã nguồn trên GitHub giúp AWS CodeBuild và AWS CodePipeline có thể tự động lấy phiên bản mới nhất của dự án mỗi khi có thay đổi, tạo tiền đề cho quy trình Continuous Integration và Continuous Deployment trong các bước tiếp theo.

### Hoàn thành

Sau khi hoàn tất các bước trên, môi trường CI/CD đã được chuẩn bị đầy đủ. Dự án đã có tệp **buildspec.yml** để mô tả quy trình Build và Deploy, đồng thời mã nguồn đã được đồng bộ lên GitHub, sẵn sàng kết nối với AWS CodeBuild và AWS CodePipeline trong các phần tiếp theo.