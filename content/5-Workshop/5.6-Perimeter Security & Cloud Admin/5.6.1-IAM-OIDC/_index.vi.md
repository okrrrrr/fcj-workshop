---
title : "Cấu hình IAM OIDC Provider và GitHub Actions"
date : 2024-01-01
weight : 1
chapter : false
pre : " <b> 5.6.1. </b> "
---

### Tạo IAM OIDC Provider cho GitHub Actions

Sau khi hoàn thành quy trình CI/CD, bước tiếp theo là thiết lập cơ chế xác thực an toàn giữa **GitHub Actions** và **AWS** thông qua **OpenID Connect (OIDC)**. Phương pháp này cho phép GitHub Actions truy cập các tài nguyên AWS bằng các thông tin xác thực tạm thời mà không cần lưu trữ **AWS Access Key** và **Secret Access Key** trong mã nguồn.

Truy cập dịch vụ **AWS Identity and Access Management (IAM)**, chọn **Identity Providers** và tạo mới một **OIDC Provider** dành cho GitHub Actions.

![](/images/5-Workshop/5.6-Perimeter-Security/image.png)

### Xác nhận OIDC Provider

Sau khi tạo thành công, kiểm tra lại danh sách **Identity Providers** để xác nhận AWS đã liên kết với địa chỉ **token.actions.githubusercontent.com**.

![](/images/5-Workshop/5.6-Perimeter-Security/image-1.png)

Việc sử dụng OIDC giúp GitHub Actions có thể xác thực trực tiếp với AWS thông qua Access Token được cấp trong quá trình thực thi Workflow, góp phần nâng cao tính bảo mật cho hệ thống.

### Tạo IAM Role cho GitHub Actions

Tiếp theo, tạo một **IAM Role** mới và lựa chọn **Trusted Entity** là **Web Identity**. IAM Role này sẽ cho phép GitHub Actions nhận quyền truy cập tạm thời vào tài khoản AWS sau khi được xác thực thành công thông qua OIDC.

![](/images/5-Workshop/5.6-Perimeter-Security/image-2.png)

Trong quá trình tạo Role, tiến hành cấp quyền **AdministratorAccess** để GitHub Actions có đủ quyền thực hiện các thao tác triển khai tài nguyên AWS trong quy trình CI/CD.

![](/images/5-Workshop/5.6-Perimeter-Security/image-3.png)

### Hoàn tất cấu hình IAM Role

Sau khi cấu hình hoàn tất, IAM Role **GitHubActions-Deploy** sẽ xuất hiện trong danh sách **IAM Roles** và sẵn sàng được sử dụng trong các Workflow của GitHub Actions.

![](/images/5-Workshop/5.6-Perimeter-Security/image-4.png)

IAM Role này sẽ được tham chiếu trong tệp cấu hình Workflow của GitHub Actions để thực hiện các tác vụ như Build, Deploy và quản lý tài nguyên AWS một cách tự động mà không cần sử dụng khóa truy cập cố định.

### Hoàn thành

Sau khi hoàn tất các bước trên, hệ thống đã thiết lập thành công cơ chế xác thực giữa GitHub Actions và AWS bằng **OpenID Connect (OIDC)**. Giải pháp này giúp tăng cường bảo mật, giảm thiểu rủi ro lộ khóa truy cập AWS và hỗ trợ quá trình triển khai ứng dụng tự động trong môi trường Cloud.