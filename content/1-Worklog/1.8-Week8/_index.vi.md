---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Tìm hiểu Data & Analytics: Redshift, Glue, Athena.
* Học cách xây dựng Data Lake với Lake Formation.
* Thực hành ETL và Business Intelligence với QuickSight.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Route 53, CloudFront từ tuần 7. Tìm hiểu Amazon Redshift: clusters, nodes, RA3 architecture. Hiểu Redshift Spectrum để query data trực tiếp từ S3. Tìm hiểu Redshift WLM (Workload Management) để optimize queries | 08/06/2026 | 08/06/2026 | <https://docs.aws.amazon.com/redshift/latest/gsg/new-user.html> |
| 3 | Tạo Redshift Cluster với dc2.large node. Configure VPC Security Group cho Redshift (mở port 5439). Kết nối cluster bằng SQL client như VS Code với extension. Tạo database và schema để organize tables. Tạo tables với distribution style (KEY, ALL, EVEN) và sort keys để optimize query performance. Load data từ S3 bằng COPY command để import data nhanh. Chạy queries để verify data đã load đúng. Monitor cluster performance trong Console để theo dõi CPU và storage | 09/06/2026 | 09/06/2026 | <https://docs.aws.amazon.com/redshift/latest/dg/tutorial-loading-data.html> |
| 4 | Tạo Glue Crawler để discover schema từ S3 data tự động. Kiểm tra Data Catalog sau khi crawler chạy xong để xem tables đã được tạo. Tạo Glue Job với PySpark để transform data giữa các formats. Viết transformation logic như filter, join, aggregate để clean data. Cấu hình job bookmark cho incremental loading để chỉ process data mới. Chạy Glue Job và monitor execution trong CloudWatch Logs. Schedule job chạy tự động với Trigger theo thời gian định sẵn. Sử dụng Glue Studio visual editor để tạo ETL job dễ dàng hơn. Tạo ETL job bằng drag-and-drop interface thay vì viết code. Preview data transformation để verify logic trước khi chạy thực tế | 10/06/2026 | 10/06/2026 | <https://000035.awsstudygroup.com/> |
| 5 | Truy cập Athena Console. Mở Query Editor để viết SQL queries. Tạo database: CREATE DATABASE analytics để organize tables. Tạo table với SerDe definition để specify data format (JSON, Parquet, etc.) cho S3 data. Chạy SELECT query để verify data có thể đọc được. Tạo views cho common queries để reuse logic. Sử dụng CTE (Common Table Expressions) để viết queries phức tạp dễ đọc hơn. Export query results sang S3 để share data với team. Đăng ký QuickSight account (enterprise version). Tạo Dataset từ Athena để connect với data source. Tạo Analysis với various charts (bar, line, pie) để visualize data. Tạo Dashboard và share với team để collaborate | 11/06/2026 | 11/06/2026 | <https://000072.awsstudygroup.com/> |
| 6 | Enable Lake Formation và set up admin permissions. Register S3 bucket làm Data Lake location để centralize storage. Tạo database và tables trong Lake Formation với fine-grained permissions. Cấu hình LF-tags cho data governance và classification. Grant permissions cho IAM users/roles để control access. Test row-level security để verify users chỉ thấy data được phép. Thiết kế Data Lake architecture với 3 layers: bronze (raw data), silver (cleaned data), gold (curated/business-ready). Tạo S3 bucket structure theo lake formation pattern. Chạy Glue Crawler để catalog raw data từ bronze layer. Tạo Glue Job transform data từ bronze → silver để clean và standardize. Tạo aggregation queries trong Athena cho reporting. Build QuickSight dashboard từ curated data để present insights | 12/06/2026 | 12/06/2026 | <https://aws.amazon.com/lake-formation/> |


### Kết quả đạt được tuần 8:

* Tạo và quản lý Redshift Cluster cho data warehousing.
* Sử dụng AWS Glue để xây dựng ETL pipelines.
* Query data serverless với Amazon Athena.
* Xây dựng Data Lake với Lake Formation và QuickSight dashboards.
