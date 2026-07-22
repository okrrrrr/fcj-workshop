---
title: "Worklog Tuần 11"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Hoàn thành project AWS Malware Detection (React + AWS Cognito + S3).
* Áp dụng AWS Well-Architected Framework để review architecture.
* Chuẩn bị demo project và báo cáo cuối khóa.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
|-----|------|------------|-----------------|-------------------|
| 2 | Ôn tập Cost Optimization từ tuần 10. Thiết kế project architecture cho Malware Detection app. Setup AWS Cognito User Pool với App Client sử dụng USER_PASSWORD_AUTH flow cho authentication. Configure Identity Pool để map Cognito users với IAM roles cho secure S3 access | 29/06/2026 | 29/06/2026 | <https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html> |
| 3 | Initialize React project với Vite + TypeScript cho frontend hiện đại. Configure Tailwind CSS cho styling. Cài AWS SDK packages (cognito-identity-provider, client-s3, s3-request-presigner). Tạo aws.ts config file để manage AWS credentials từ environment variables. Implement cognitoService.ts với các functions signUp, signIn, signOut, forgotPassword, confirmSignUp, refreshTokens sử dụng USER_PASSWORD_AUTH flow | 30/06/2026 | 30/06/2026 | <https://docs.amplify.aws/react/build-a-backend/auth/> |
| 4 | Tạo tokenService.ts với TokenManager class để handle token storage (sessionStorage + cookies), auto token refresh trước khi hết hạn, token validation, và listener pattern cho auth state changes. Tạo AuthContext.tsx với React Context API để manage auth state (user, isLoading, error) và cung cấp signUp, signIn, signOut, forgotPassword methods. Implement LoginPage, RegisterPage, ForgotPasswordPage với form validation và error handling cho từng auth flow | 01/07/2026 | 01/07/2026 | <https://docs.aws.amazon.com/cognito/latest/developerguide/amazon-cognito-user-pools-using-tokens.html> |
| 5 | Tạo S3 bucket với CORS configuration cho cross-origin requests. Implement s3Service.ts với các functions getPresignedUploadUrl, getPresignedDownloadUrl, uploadFileToS3 (sử dụng XHR cho progress tracking), deleteFileFromS3, listFiles, checkFileExists. Tạo FileUpload component với drag & drop interface, file validation (size limit 100MB, file types), progress bar, file list display, và security info section. Tạo DashboardPage với stats cards (total files, safe, malware, scanning), tab navigation (Upload/History), và analysis result display | 02/07/2026 | 02/07/2026 | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html> |
| 6 | Responsive design với Tailwind CSS cho mobile/desktop. Error handling và loading states across all pages. Performance optimization với lazy loading patterns. Security hardening (input validation, file type sanitization, XSS protection). Tạo AWS_SETUP_GUIDE.md documentation với step-by-step Cognito và S3 setup instructions. Chuẩn bị README.md với project overview, installation, configuration, và architecture. Vẽ architecture diagram thể hiện React frontend kết nối với AWS Cognito và S3 | 03/07/2026 | 03/07/2026 | <https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html> |


### Kết quả đạt được tuần 11:

* Hoàn thành ứng dụng React với AWS Cognito authentication (USER_PASSWORD_AUTH flow).
* Tích hợp AWS S3 cho file upload/download với presigned URLs và progress tracking.
* Áp dụng AWS Well-Architected Framework để review architecture.
* Chuẩn bị demo project với architecture diagram và presentation slides.