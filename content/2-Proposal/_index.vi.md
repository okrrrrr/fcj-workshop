---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

Tại phần này, bạn cần tóm tắt các nội dung trong workshop mà bạn **dự tính** sẽ làm.

# Serverless AI Malware Sandbox & Analysis Platform  
## Môi trường Sandbox cô lập và phân tích mã độc tự động tích hợp AI trên đám mây  


### 1. Tóm tắt điều hành  
Dự án **Serverless AI Malware Sandbox & Analysis Platform** được thiết kế nhằm xây dựng một môi trường kiểm thử và phân tích mã độc tự động, an toàn và tối ưu chi phí trên đám mây AWS. Nền tảng cho phép người dùng đăng ký/đăng nhập an toàn để tải lên các tệp nghi ngờ độc hại trực tiếp lên bộ lưu trữ đám mây qua API Gateway và Lambda Presigned URL. Hệ thống sử dụng hàng đợi SQS kết hợp Step Functions để xếp hàng và điều phối luồng xử lý bất đồng bộ, đưa tệp tin vào mạng Sandbox (VPC) cô lập hoàn toàn (không có Internet) để chạy mô hình AI phân tích hành vi mã độc trên máy ảo EC2. Lịch sử và kết quả quét được lưu trữ trên DynamoDB và hiển thị trực quan thông qua bảng điều khiển Web host trên AWS Amplify. Nền tảng áp dụng các tiêu chuẩn an ninh nghiêm ngặt bao gồm AWS WAF bảo vệ cổng API, mã hóa dữ liệu KMS, két sắt lưu Secrets Manager và cơ chế tự động sửa lỗi cấu hình AWS Config Auto-remediation.


### 2. Tuyên bố vấn đề  
*Vấn đề hiện tại*  
Việc phân tích các tệp tin nghi ngờ độc hại thường yêu cầu thiết lập các phòng thí nghiệm phần cứng cục bộ tốn kém hoặc sử dụng các sandbox chia sẻ công cộng tiềm ẩn nguy cơ rò rỉ thông tin nhạy cảm. Đồng thời, phân tích thủ công mất nhiều thời gian, dễ gây quá tải hệ thống nếu có số lượng lớn tệp tải lên cùng lúc mà không có cơ chế xếp hàng. Ngoài ra, việc duy trì hệ thống máy ảo phân tích hoạt động liên tục 24/7 trên đám mây gây lãng phí ngân sách lớn cho các tổ chức nhỏ hoặc nhóm nghiên cứu.  


*Giải pháp*  
Nền tảng giải quyết các vấn đề trên thông qua sự kết hợp của AWS Serverless, mạng Sandbox cô lập và mô hình AI tự động:  
- **Xác thực & Tải lên an toàn**: Amazon Cognito quản lý tài khoản người dùng an toàn. Amazon S3 cho phép client tải tệp trực tiếp qua Presigned URL để tránh nghẽn luồng xử lý.  
- **Backend Serverless & Xếp hàng**: AWS Lambda và API Gateway xử lý logic nghiệp vụ nhanh chóng. Hàng đợi Amazon SQS kết hợp Step Functions giúp điều phối, xếp hàng các yêu cầu phân tích, ngăn ngừa quá tải hệ thống.  
- **Sandbox cô lập chạy mô hình AI**: Amazon VPC thiết kế mạng Private Subnets cô lập hoàn toàn (không có cổng Internet) kết hợp VPC Endpoints. Máy ảo EC2 (hoặc ECS) chạy mô hình học máy phân tích tệp an toàn và lưu log phân tích qua CloudWatch.  
- **Cơ sở dữ liệu & Tự động hóa**: Cơ sở dữ liệu NoSQL DynamoDB lưu trữ lịch sử quét. Luồng CI/CD tự động bằng AWS CodePipeline & CodeBuild. Cài đặt tính năng S3 Lifecycle tự động xóa tệp độc hại sau 7 ngày để giải phóng bộ nhớ và đảm bảo an toàn.  
- **Bảo mật chu vi & Kiểm toán**: AWS WAF bảo vệ cổng kết nối khỏi spam API, AWS KMS mã hóa toàn bộ dữ liệu lưu trữ, AWS Secrets Manager lưu mật khẩu bảo mật, và cặp đôi AWS Config & EventBridge tự động phát hiện, khóa kín S3 bucket trong 1 giây nếu có người vô tình mở Public (Auto-remediation).  


*Lợi ích và hoàn vốn đầu tư (ROI)*  
Giải pháp cung cấp một môi trường phân tích tự động hóa giúp rút ngắn thời gian kiểm thử từ hàng giờ xuống hàng phút với độ an toàn dữ liệu tuyệt đối nhờ Sandbox cô lập. Chi phí vận hành tối ưu vượt trội nhờ cơ chế tắt/mở tài nguyên thông minh (chỉ bật máy ảo EC2 khi có tệp trong hàng đợi cần phân tích), giúp giảm chi phí hạ tầng từ **51,40 USD/tháng** (nếu chạy 24/7) xuống chỉ còn **5,20 USD/tháng** (chỉ bật khi kiểm thử thực tế). Thời gian hoàn vốn dự kiến 3–6 tháng nhờ tiết kiệm thời gian vận hành thủ công và chi phí bản quyền phần mềm phân tích mã độc thương mại.  


### 3. Kiến trúc giải pháp  
Hệ thống sử dụng kiến trúc phân lớp hướng sự kiện và Serverless đảm bảo tính cô lập và hiệu năng cao. Dữ liệu từ Web client đi qua Cognito xác thực, gọi Lambda qua API Gateway để lấy Presigned URL, sau đó tải trực tiếp lên S3 bucket thô. Sự kiện tệp tin mới kích hoạt SQS xếp hàng và Step Functions điều phối việc khởi động máy ảo EC2 trong VPC Sandbox không có Internet để mô hình AI quét tệp an toàn qua VPC Endpoint kết nối S3 và ghi log kết quả quét vào DynamoDB.  

![Architecture Diagram](/images/2-Proposal/architecture-diagram.png)  


*Dịch vụ AWS sử dụng*  
- **Amazon Cognito**: Quản lý đăng ký, đăng nhập và phân quyền truy cập cho người dùng.  
- **Amazon S3**: Lưu trữ tệp thô tải lên và cấu hình Lifecycle dọn rác tự động sau 7 ngày.  
- **Amazon API Gateway & AWS Lambda**: Cung cấp cổng API và chạy mã nguồn Python xử lý sinh URL/quét lịch sử.  
- **Amazon SQS & Step Functions**: Quản lý hàng đợi tệp tin và điều phối quy trình phân tích bất đồng bộ.  
- **Amazon DynamoDB**: Lưu trữ lịch sử quét và kết quả phân tích hành vi của tệp tin.  
- **Amazon VPC**: Tạo mạng Sandbox cô lập hoàn toàn không có cổng Internet (Private Subnets, VPC Endpoints).  
- **Amazon EC2 (hoặc ECS)**: Chạy mô hình AI phân tích mã độc trong Sandbox.  
- **AWS CodePipeline & CodeBuild**: Tự động hóa quy trình CI/CD từ GitHub lên môi trường AWS.  
- **AWS Amplify**: Kết nối kho Git Hugo để tự động host giao diện trang web báo cáo.  
- **AWS WAF**: Tường lửa bảo vệ cổng API Gateway khỏi các cuộc tấn công và rate limit chặn spam IP.  
- **AWS Secrets Manager & KMS**: Lưu trữ mật mã tập trung và mã hóa toàn bộ dữ liệu lưu trữ.  
- **AWS Config & EventBridge**: Giám sát cấu hình bảo mật đám mây và tự động sửa lỗi cấu hình sai.  
- **Amazon CloudWatch & CloudTrail**: Lưu trữ log tiến trình phân tích AI và ghi log lịch sử thao tác hệ thống.  


*Thiết kế thành phần*  
- **Thiết bị Biên & Client**: Giao diện Web gọi API Gateway, thực hiện xác thực qua Cognito và tải tệp lên S3 qua Presigned URL.  
- **Hệ thống API Backend**: API Gateway chuyển yêu cầu tới Lambda. Lambda xử lý nghiệp vụ chính và đẩy sự kiện tệp mới vào SQS.  
- **Hàng đợi & Điều phối**: SQS lưu giữ sự kiện, Step Functions kiểm soát trạng thái máy ảo EC2, đảm bảo chỉ bật máy ảo chạy AI khi có tệp cần xử lý và tắt đi khi hoàn thành.  
- **Sandbox an sau**: Mạng VPC cô lập hoàn toàn ngăn mã độc kết nối với máy chủ điều khiển của tin tặc (C2 server).  
- **Tự động dọn rác**: S3 Lifecycle rule xóa sạch tệp độc hại định kỳ sau 7 ngày.  


### 4. Triển khai kỹ thuật  
*Các giai đoạn triển khai*  
Dự án được chia thành 4 giai đoạn chính trong kỳ thực tập:  
1. **Nghiên cứu & Thiết kế kiến trúc (Cuối tháng 4)**: Nghiên cứu các giải pháp sandbox và thiết kế chi tiết mạng VPC Sandbox cô lập cùng luồng xử lý bất đồng bộ.  
2. **Thiết lập hạ tầng & CI/CD (Tháng 5)**: Sử dụng AWS console/CDK thiết lập VPC, S3, DynamoDB, Cognito và luồng CI/CD CodePipeline tự động từ GitHub.  
3. **Phát triển module AI & Backend (Tháng 6)**: Cấu hình mô hình AI trên máy ảo EC2 Sandbox, viết mã nguồn Lambda xử lý logic và tích hợp Cognito xác thực vào Frontend.  
4. **Tối ưu hóa bảo mật & Kiểm thử (Tháng 7)**: Cấu hình WAF, KMS, thiết lập AWS Config Auto-remediation để tự động sửa lỗi bảo mật, thực hiện kiểm thử tải hệ thống và bàn giao.  


*Yêu cầu kỹ thuật*  
- **Môi trường Sandbox**: VPC cô lập hoàn toàn, sử dụng VPC Endpoints (Interface/Gateway) cho S3, DynamoDB và CloudWatch để truyền dữ liệu nội bộ an toàn.  
- **Hệ thống AI**: Máy ảo EC2 (cấu hình t3.medium) được cài đặt các công cụ phân tích tệp độc hại và mô hình AI nhận diện hành vi tệp tin.  
- **Backend & CI/CD**: Viết code Python cho Lambda sử dụng AWS SDK (Boto3). Thiết lập các file cấu hình buildspec cho CodeBuild để tự động đóng gói code mới khi push lên GitHub.  


### 5. Lộ trình & Mốc triển khai  
- **Trước thực tập (Trước 20/04)**: Lên kế hoạch dự án, nghiên cứu lý thuyết Sandbox và vẽ sơ đồ kiến trúc hệ thống đám mây.  
- **Trong thời gian thực tập (20/04 – 25/07)**:  
    - **Cuối tháng 4**: Học hạ tầng AWS và triển khai thiết lập môi trường Sandbox VPC cô lập.  
    - **Tháng 5**: Triển khai API Lambda, tích hợp SQS, DynamoDB, Cognito và luồng CI/CD tự động.  
    - **Tháng 6**: Cài đặt mô hình AI lên Sandbox EC2, hoàn thiện giao diện Web.  
    - **Tháng 7**: Kiểm thử hệ thống an ninh toàn diện, tối ưu hóa chi phí hạ tầng và bàn giao vận hành trước ngày 25/07.  
- **Sau triển khai (Sau 25/07)**: Tiếp tục vận hành thử nghiệm và nghiên cứu nâng cấp tính năng trong vòng 1 năm.  


### 6. Ước tính ngân sách  
Bảng ngân sách chi tiết dựa trên [AWS Pricing Calculator](https://calculator.aws/):  


*Chi phí hạ tầng (Tối ưu hóa chạy thử nghiệm)*  
- **Amazon EC2 (t3.medium)**: Máy ảo chạy AI trong Sandbox. Giá chạy 24/7: ~33.00 USD/tháng. Giá tối ưu (chỉ bật khi test): **~2.50 USD/tháng**.  
- **AWS WAF**: Tường lửa bảo vệ API Gateway. Giá chạy 24/7: ~7.00 USD/tháng. Giá tối ưu (chỉ bật khi test): **~0.50 USD/tháng**.  
- **VPC Endpoints**: Cổng kết nối nội bộ Sandbox. Giá chạy 24/7: ~9.00 USD/tháng. Giá tối ưu (chỉ bật khi test): **~0.60 USD/tháng**.  
- **AWS KMS**: Khóa mã hóa dữ liệu. Giá chạy 24/7: ~1.00 USD/tháng. Giá tối ưu: **~1.00 USD/tháng**.  
- **AWS Secrets Manager**: Két sắt lưu mật khẩu. Giá chạy 24/7: ~0.40 USD/tháng. Giá tối ưu: **~0.40 USD/tháng**.  
- **AWS Config**: Giám sát cấu hình tự động. Giá chạy 24/7: ~1.00 USD/tháng. Giá tối ưu: **~0.20 USD/tháng**.  
- **Các dịch vụ serverless khác (S3, Lambda, API Gateway, SQS, DynamoDB, Amplify)**: Được bao phủ hoàn toàn trong gói **AWS Free Tier** (Miễn phí cho quy mô phát triển/thử nghiệm).  


*Tổng chi phí ước tính*:  
- **Vận hành chạy 24/7**: ~51.40 USD/tháng (~1.250.000đ/tháng)  
- **Tối ưu hóa chạy thử nghiệm (Chỉ bật khi test)**: **~5.20 USD/tháng** (~125.000đ/tháng)  


### 7. Đánh giá rủi ro  
*Ma trận rủi ro*  
- **Rò rỉ mã độc ra Internet**: Ảnh hưởng cực cao, xác suất cực thấp (nhờ thiết kế VPC Sandbox cô lập hoàn toàn).  
- **Vượt quá ngân sách do quên tắt máy ảo EC2**: Ảnh hưởng trung bình, xác suất trung bình (nếu bật EC2 liên tục).  
- **Tấn công spam tải tệp lên hệ thống**: Ảnh hưởng trung bình, xác suất trung bình.  


*Chiến lược giảm thiểu*  
- **Rò rỉ mạng**: Cấm hoàn toàn Internet Gateway trong VPC Sandbox, cấu hình Security Groups và Network ACLs chỉ cho phép kết nối nội bộ.  
- **Chi phí**: Thiết lập script tự động tắt máy ảo EC2 sau 30 phút không hoạt động, cài đặt cảnh báo ngân sách AWS Budget gửi cảnh báo khi chi phí vượt quá 5 USD.  
- **Tấn công spam**: Cấu hình luật AWS WAF rate limiting chặn IP spam và giới hạn kích thước tệp tải lên tối đa trên S3 (ví dụ tối đa 10MB).  


*Kế hoạch dự phòng*  
- Sử dụng AWS CloudFormation/CDK để nhanh chóng khôi phục toàn bộ kiến trúc hạ tầng nếu gặp lỗi cấu hình nghiêm trọng.  


### 8. Kết quả kỳ vọng  
*Cải tiến kỹ thuật*: Xây dựng thành công hệ thống Sandbox phân tích mã độc tự động, an toàn và khép kín hoàn toàn trên đám mây AWS.  
*Giá trị dài hạn*: Cung cấp công cụ phân tích tệp tin an toàn cho tổ chức, tích lũy kinh nghiệm triển khai kiến trúc DevSecOps cao cấp trên môi trường đám mây AWS.
