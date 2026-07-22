---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# VPC ENDPOINT — CHÌA KHÓA ĐỂ XÂY SANDBOX CÔ LẬP TRÊN AWS


## Chuyện là...


Khi nhóm mình bắt tay vào xây dựng hệ thống phân tích mã độc trên AWS, yêu cầu đầu tiên mà anh mentor đặt ra rất rõ ràng: **"Máy ảo chạy AI phân tích file phải nằm trong một mạng hoàn toàn cô lập, không được phép kết nối Internet dưới bất kỳ hình thức nào."**


Nghe thì đơn giản — cứ bỏ Internet Gateway ra khỏi VPC là xong chứ gì? Nhưng thực tế không dễ như vậy. Khi mình xóa Internet Gateway, con EC2 trong Sandbox mất kết nối với **tất cả** dịch vụ AWS bên ngoài — kể cả S3 (nơi chứa file cần quét), DynamoDB (nơi ghi kết quả), và CloudWatch Logs (nơi ghi log tiến trình AI). Kết quả là máy ảo chạy mô hình AI xong nhưng... im lặng hoàn toàn, không ghi được gì ra ngoài cả.


Đó là lúc mình phát hiện ra **VPC Endpoint** — giải pháp cho phép các tài nguyên bên trong VPC giao tiếp với dịch vụ AWS mà không cần đi qua Internet.


## VPC Endpoint là gì?


Nói đơn giản, VPC Endpoint giống như một **đường hầm riêng** nối thẳng từ VPC của bạn tới một dịch vụ AWS cụ thể, hoàn toàn đi qua mạng nội bộ của AWS (AWS PrivateLink). Traffic không bao giờ rời khỏi backbone của Amazon.


Có **2 loại** VPC Endpoint:


### 1. Gateway Endpoint (Miễn phí 💰)
- Chỉ hỗ trợ **S3** và **DynamoDB**
- Hoạt động bằng cách thêm một route entry vào Route Table của subnet
- **Không tốn phí** — đây là điểm cực kỳ quan trọng khi tối ưu ngân sách
- Cấu hình đơn giản: chỉ cần tạo endpoint, chọn route table, xong


### 2. Interface Endpoint (Tốn phí theo giờ + data)
- Hỗ trợ **hầu hết các dịch vụ AWS còn lại** (CloudWatch Logs, SQS, EC2 API, SSM, KMS...)
- Hoạt động bằng cách tạo một **Elastic Network Interface (ENI)** trong subnet của bạn với private IP
- Phí khoảng **~$0.01/giờ/AZ** + phí data transfer
- Cần bật **Private DNS** để các SDK/CLI tự động resolve đúng endpoint


## Kiến trúc Sandbox của nhóm mình


![VPC Endpoint Architecture](/images/3-Blog/blog1_vpc_endpoint.png)


Như hình trên, đây là kiến trúc mạng Sandbox mà nhóm mình thiết kế:


- **VPC Sandbox** chỉ có Private Subnets, **không có Internet Gateway, không có NAT Gateway**
- EC2 instance chạy mô hình AI nằm hoàn toàn bên trong
- Kết nối với các dịch vụ AWS qua 3 VPC Endpoint:
  - **S3 Gateway Endpoint**: Để EC2 đọc file cần phân tích và ghi kết quả (miễn phí)
  - **DynamoDB Gateway Endpoint**: Để ghi lịch sử quét vào database (miễn phí)
  - **CloudWatch Logs Interface Endpoint**: Để ghi log tiến trình AI (~$7/tháng cho 1 AZ)


## Lỗi mà mình đã gặp


### Lỗi 1: Quên bật Private DNS cho Interface Endpoint


Khi tạo Interface Endpoint cho CloudWatch Logs, mình quên tick vào ô **"Enable Private DNS Name"**. Kết quả là Boto3 SDK trong EC2 vẫn cố resolve `logs.ap-southeast-1.amazonaws.com` ra public IP → timeout → không ghi được log.


**Fix:** Bật Private DNS trong cấu hình endpoint. Lưu ý: VPC phải bật `enableDnsSupport` và `enableDnsHostnames` trước.


### Lỗi 2: Security Group của Interface Endpoint chặn traffic


Interface Endpoint tạo ra một ENI, và ENI đó có Security Group riêng. Mình quên mở port **443 (HTTPS)** cho ENI → EC2 không gọi được API.


**Fix:** Tạo Security Group cho endpoint cho phép inbound TCP 443 từ CIDR của Sandbox subnet.


### Lỗi 3: S3 Gateway Endpoint nhưng quên gắn vào đúng Route Table


Gateway Endpoint hoạt động bằng route table. Mình tạo endpoint nhưng gắn vào Main Route Table, trong khi subnet của EC2 đang dùng Custom Route Table riêng.


**Fix:** Khi tạo S3 Gateway Endpoint, chọn đúng route table mà subnet đang associate.


## Chi phí thực tế


| Endpoint | Loại | Phí/tháng |
|---|---|---|
| S3 | Gateway | **$0.00** |
| DynamoDB | Gateway | **$0.00** |
| CloudWatch Logs | Interface | **~$7.20** (1 AZ) |
| **Tổng** | | **~$7.20/tháng** |


Nếu chỉ bật khi test (khoảng 2 giờ/ngày), chi phí giảm xuống còn khoảng **$0.60/tháng**.


## Bài học rút ra


VPC Endpoint là thành phần **bắt buộc** nếu bạn muốn xây dựng bất kỳ workload nào trong private subnet mà vẫn cần tương tác với dịch vụ AWS. Mình rút ra mấy điều:


1. **Luôn ưu tiên Gateway Endpoint** cho S3 và DynamoDB vì miễn phí
2. **Kiểm tra Private DNS** ngay sau khi tạo Interface Endpoint — đây là nguyên nhân #1 gây lỗi kết nối
3. **Security Group của ENI** dễ bị quên — nhớ mở port 443
4. **Route Table phải match** — đặc biệt khi dùng custom route table cho subnet


Hy vọng bài viết giúp bạn tránh được mấy cái "hố" mà mình đã rơi vào. Nếu bạn đang xây sandbox, isolated workload, hay bất kỳ hệ thống nào cần private connectivity trên AWS — VPC Endpoint chính là thứ bạn cần tìm hiểu đầu tiên.


---
