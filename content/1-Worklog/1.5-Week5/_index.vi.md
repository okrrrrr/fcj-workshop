---
title: "Worklog Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Tìm hiểu Docker và Container trên AWS.
* Học cách triển khai ứng dụng container với ECS và EKS.
* Thực hành Infrastructure as Code với CloudFormation và CDK.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập CloudWatch, CloudTrail từ tuần 4. Tìm hiểu Docker cơ bản: images, containers, registries. Hiểu Dockerfile và cách build image. Tìm hiểu Docker Compose để quản lý multi-container | 18/05/2026 | 18/05/2026 | <https://docs.docker.com/get-started/introduction/> |
| 3 | Cài đặt Docker Desktop trên Windows. Kiểm tra version docker. Tạo Dockerfile đơn giản với nginx image. Build image: docker build -t my-app. Run container: docker run -d -p 8080:80 my-app. Push image lên Docker Hub để share với team. Tạo docker-compose.yml với web app và database services. Chạy docker-compose up -d để khởi tạo tất cả containers. Kiểm tra containers đang chạy với docker ps | 19/05/2026 | 19/05/2026 | <https://000067.awsstudygroup.com/3-containersanddocker/> |
| 4 | Tạo ECR Repository để lưu trữ Docker images private. Push Docker image lên ECR sử dụng AWS credentials. Tạo ECS Cluster với Fargate launch type (serverless container). Tạo Task Definition với container configuration. Tạo Service với Load Balancer để distribute traffic. Cấu hình Security Group cho container. Kiểm tra service đang chạy và xem logs trong CloudWatch. Scale service bằng cách tăng desired count lên 2 | 20/05/2026 | 20/05/2026 | <https://000016.awsstudygroup.com/> |
| 5 | Tạo EKS Cluster với eksctl command line tool. Cấu hình kubeconfig: aws eks update-kubeconfig --name my-cluster. Tạo Node Group với EC2 instances để run pods. Deploy sample app: kubectl apply -f deployment.yaml. Tạo Service để expose app ra ngoài. Kiểm tra pods: kubectl get pods. Scale deployment: kubectl scale deployment my-app --replicas=3. Cài đặt CDK: npm install -g aws-cdk. Tạo new project: cdk init app --language python. Viết code Python định nghĩa infrastructure. Deploy S3 bucket: cdk deploy | 21/05/2026 | 21/05/2026 | <https://www.eksworkshop.com/> |
| 6 | Viết CloudFormation Template (YAML) định nghĩa VPC với subnets. Thêm EC2 Instance và Security Group vào template. Thêm S3 Bucket với bucket policy. Upload template lên CloudFormation Console. Create Stack và theo dõi creation progress. Kiểm tra Outputs sau khi stack hoàn thành để lấy resource IDs. Tạo Docker image cho web application với multi-stage build. Push image lên Amazon ECR. Tạo ECS Cluster với Fargate. Deploy container với ALB integration để route HTTP traffic. Test ứng dụng qua ALB DNS | 22/05/2026 | 22/05/2026 | <https://000067.awsstudygroup.com/2-prerequiste/2.1-createcloudformation/> |


### Kết quả đạt được tuần 5:

* Hiểu và sử dụng Docker để build, run và push container images.
* Triển khai ứng dụng container với Amazon ECS Fargate.
* Tạo Kubernetes cluster với Amazon EKS và deploy ứng dụng.
* Viết Infrastructure as Code với CloudFormation và CDK.
