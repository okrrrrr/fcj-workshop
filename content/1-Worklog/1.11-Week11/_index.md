---
title: "Week 11 Worklog"
date: 2026-06-29
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Objectives:

* Complete AWS Malware Detection project (React + AWS Cognito + S3).
* Apply AWS Well-Architected Framework to review architecture.
* Prepare project demo and final report.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
|-----|------|------------|-----------------|-------------------|
| 2 | Reviewed Cost Optimization from Week 10. Designed project architecture for Malware Detection app. Set up AWS Cognito User Pool with App Client using USER_PASSWORD_AUTH flow for authentication. Configured Identity Pool to map Cognito users with IAM roles for secure S3 access | 29/06/2026 | 29/06/2026 | <https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html> |
| 3 | Initialized React project with Vite + TypeScript for modern frontend. Configured Tailwind CSS for styling. Installed AWS SDK packages (cognito-identity-provider, client-s3, s3-request-presigner). Created aws.ts config file to manage AWS credentials from environment variables. Implemented cognitoService.ts with signUp, signIn, signOut, forgotPassword, confirmSignUp, refreshTokens functions using USER_PASSWORD_AUTH flow | 30/06/2026 | 30/06/2026 | <https://docs.amplify.aws/react/build-a-backend/auth/> |
| 4 | Created tokenService.ts with TokenManager class to handle token storage (sessionStorage + cookies), auto token refresh before expiration, token validation, and listener pattern for auth state changes. Created AuthContext.tsx with React Context API to manage auth state (user, isLoading, error) and provide signUp, signIn, signOut, forgotPassword methods. Implemented LoginPage, RegisterPage, ForgotPasswordPage with form validation and error handling for each auth flow | 01/07/2026 | 01/07/2026 | <https://docs.aws.amazon.com/cognito/latest/developerguide/amazon-cognito-user-pools-using-tokens.html> |
| 5 | Created S3 bucket with CORS configuration for cross-origin requests. Implemented s3Service.ts with getPresignedUploadUrl, getPresignedDownloadUrl, uploadFileToS3 (using XHR for progress tracking), deleteFileFromS3, listFiles, checkFileExists functions. Created FileUpload component with drag & drop interface, file validation (size limit 100MB, file types), progress bar, file list display, and security info section. Created DashboardPage with stats cards (total files, safe, malware, scanning), tab navigation (Upload/History), and analysis result display | 02/07/2026 | 02/07/2026 | <https://docs.aws.amazon.com/AmazonS3/latest/userguide/upload-objects.html> |
| 6 | Implemented responsive design with Tailwind CSS for mobile/desktop compatibility. Added error handling and loading states across all pages. Applied performance optimization with lazy loading patterns. Implemented security hardening (input validation, file type sanitization, XSS protection). Created AWS_SETUP_GUIDE.md documentation with step-by-step Cognito and S3 setup instructions. Prepared README.md with project overview, installation, configuration, and architecture. Designed architecture diagram showing React frontend connecting to AWS Cognito and S3 | 03/07/2026 | 03/07/2026 | <https://docs.aws.amazon.com/wellarchitected/latest/framework/welcome.html> |


### Week 11 Achievements:

* Completed React application with AWS Cognito authentication (USER_PASSWORD_AUTH flow).
* Integrated AWS S3 for file upload/download with presigned URLs and progress tracking.
* Applied AWS Well-Architected Framework to review architecture.
* Prepared project demo with architecture diagram and presentation slides.