---
title: "Worklog Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Tìm hiểu Networking & CDN: Route 53, CloudFront.
* Học cách bảo mật ứng dụng với AWS WAF và Shield.
* Thực hành triển khai CDN và bảo mật cho website.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Lambda, Step Functions từ tuần 6. Tìm hiểu Route 53: hosted zones, record sets, routing policies. Hiểu DNS failover và health checks. Tìm hiểu các loại record: A, AAAA, CNAME, MX, TXT | 01/06/2026 | 01/06/2026 | <https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/Welcome.html> |
| 3 | Tạo Hosted Zone trong Route 53 để quản lý DNS cho domain. Tạo A Record trỏ đến ALB endpoint để route traffic đến load balancer. Tạo CNAME Record cho www subdomain redirect đến root domain. Cấu hình Health Check để monitor endpoint availability. Tạo Failover record với primary target là EC2 và secondary là S3 để đảm bảo high availability. Cập nhật nameservers tại domain registrar để trỏ về Route 53. Verify DNS propagation bằng dig hoặc nslookup | 02/06/2026 | 02/06/2026 | <https://000010.awsstudygroup.com/> |
| 4 | Truy cập CloudFront Console. Tạo Distribution mới với origin là S3 bucket hoặc ALB. Cấu hình Default Cache Behavior với viewer protocol policy (HTTPS only). Thêm Price Class để chọn edge locations phù hợp (All Locations hoặc specific regions). Cấu hình TTL (Minimum, Maximum, Default) để control cache duration. Enable CloudFront Functions để manipulate requests và responses tại edge. Test distribution qua CloudFront URL và verify caching hoạt động bằng header inspection | 03/06/2026 | 03/06/2026 | <https://000130.awsstudygroup.com/> |
| 5 | Request SSL/TLS Certificate từ ACM (AWS Certificate Manager). Validate domain bằng DNS validation method. Thêm CNAME record vào Route 53 để complete validation tự động. Gắn certificate vào CloudFront Distribution. Enable HTTPS cho viewer requests. Redirect HTTP sang HTTPS để enforce secure connection. Tạo Web ACL trong AWS WAF để define security rules. Thêm rule chặn SQL Injection attacks. Thêm rule chặn XSS (Cross-Site Scripting) attacks. Thêm rule chặn IP addresses từ blocklist. Associate WAF ACL với CloudFront Distribution để protect website | 04/06/2026 | 04/06/2026 | <https://000026.awsstudygroup.com/> |
| 6 | Enable AWS Shield Standard (miễn phí) cho CloudFront để protect against DDoS. Hiểu các protection features của Shield Standard như volumetric attack mitigation. Tạo Web ACL với Rate-based rule để limit requests per IP (ngăn chặn abuse). Cấu hình AWS Firewall Manager policy để centrally manage WAF rules. Thêm Rule Group cho common attacks patterns. Tạo S3 bucket với static website hosting enabled. Tạo CloudFront Distribution với OAI (Origin Access Identity) để restrict bucket access. Request ACM certificate cho custom domain. Configure Route 53 với A record trỏ đến CloudFront. Attach WAF Web ACL với CloudFront để filter malicious traffic. Test HTTPS và verify SSL certificate hoạt động đúng | 05/06/2026 | 05/06/2026 | <https://000026.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Cấu hình Route 53 với DNS failover và health checks.
* Triển khai CloudFront CDN với caching và edge functions.
* Thiết lập SSL/TLS certificate với ACM cho custom domain.
* Bảo mật ứng dụng với AWS WAF (SQL Injection, XSS protection).
* Bật AWS Shield Standard để protect against DDoS attacks.
