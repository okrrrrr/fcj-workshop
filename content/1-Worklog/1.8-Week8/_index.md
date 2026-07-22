---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

* Learn Data & Analytics: Redshift, Glue, Athena.
* Learn how to build Data Lake with Lake Formation.
* Practice ETL and Business Intelligence with QuickSight.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Route 53, CloudFront from Week 7. Learned about Amazon Redshift: clusters, nodes, RA3 architecture. Understood Redshift Spectrum to query data directly from S3. Learned Redshift WLM (Workload Management) to optimize queries | 08/06/2026 | 08/06/2026 | <https://docs.aws.amazon.com/redshift/latest/gsg/new-user.html> |
| 3 | Created Redshift Cluster with dc2.large node. Configured VPC Security Group for Redshift (open port 5439). Connected cluster using SQL client like VS Code with extension. Created database and schema to organize tables. Created tables with distribution style (KEY, ALL, EVEN) and sort keys to optimize query performance. Loaded data from S3 using COPY command for fast data import. Ran queries to verify data loaded correctly. Monitored cluster performance in Console to track CPU and storage | 09/06/2026 | 09/06/2026 | <https://docs.aws.amazon.com/redshift/latest/dg/tutorial-loading-data.html> |
| 4 | Created Glue Crawler to discover schema from S3 data automatically. Checked Data Catalog after crawler runs to see tables created. Created Glue Job with PySpark to transform data between formats. Wrote transformation logic like filter, join, aggregate to clean data. Configured job bookmark for incremental loading to only process new data. Ran Glue Job and monitored execution in CloudWatch Logs. Scheduled job to run automatically with Trigger at predetermined times. Used Glue Studio visual editor to create ETL jobs more easily. Created ETL job using drag-and-drop interface instead of writing code. Previewed data transformation to verify logic before actual run | 10/06/2026 | 10/06/2026 | <https://000035.awsstudygroup.com/> |
| 5 | Accessed Athena Console. Opened Query Editor to write SQL queries. Created database: CREATE DATABASE analytics to organize tables. Created table with SerDe definition to specify data format (JSON, Parquet, etc.) for S3 data. Ran SELECT query to verify data is readable. Created views for common queries to reuse logic. Used CTE (Common Table Expressions) to write complex queries more readably. Exported query results to S3 to share data with team. Registered QuickSight account (enterprise version). Created Dataset from Athena to connect with data source. Created Analysis with various charts (bar, line, pie) to visualize data. Created Dashboard and shared with team to collaborate | 11/06/2026 | 11/06/2026 | <https://000072.awsstudygroup.com/> |
| 6 | Enabled Lake Formation and set up admin permissions. Registered S3 bucket as Data Lake location to centralize storage. Created database and tables in Lake Formation with fine-grained permissions. Configured LF-tags for data governance and classification. Granted permissions for IAM users/roles to control access. Tested row-level security to verify users only see permitted data. Designed Data Lake architecture with 3 layers: bronze (raw data), silver (cleaned data), gold (curated/business-ready). Created S3 bucket structure following lake formation pattern. Ran Glue Crawler to catalog raw data from bronze layer. Created Glue Job transform data from bronze to silver to clean and standardize. Created aggregation queries in Athena for reporting. Built QuickSight dashboard from curated data to present insights | 12/06/2026 | 12/06/2026 | <https://aws.amazon.com/lake-formation/> |


### Week 8 Achievements:

* Created and managed Redshift Cluster for data warehousing.
* Used AWS Glue to build ETL pipelines.
* Queried data serverlessly with Amazon Athena.
* Built Data Lake with Lake Formation and QuickSight dashboards.
