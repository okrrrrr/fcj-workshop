---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# S3 PRESIGNED URL — UPLOAD FILE AN TOÀN MÀ KHÔNG CẦN ĐI QUA SERVER


## Bài toán thực tế


Dự án của nhóm mình là một nền tảng phân tích mã độc — người dùng cần upload file nghi ngờ lên hệ thống để AI quét. Ban đầu, flow upload mà mình thiết kế rất "thẳng tắp":


```
Client → API Gateway → Lambda → ghi file vào S3
```


Chạy thử với file nhỏ vài KB thì mượt mà. Nhưng khi test với file 15MB — **boom**, Lambda trả về lỗi `413 Payload Too Large`. Hóa ra API Gateway có giới hạn payload tối đa **10MB**, và Lambda thì giới hạn **6MB** cho request body đồng bộ.


Mình ngồi Google một lúc và phát hiện ra rằng hầu hết các hệ thống production trên AWS đều không upload file qua Lambda. Thay vào đó, họ dùng một kỹ thuật gọi là **Presigned URL**.


## Presigned URL là gì?


Presigned URL là một URL tạm thời do AWS SDK tạo ra, cho phép bất kỳ ai có URL đó thực hiện một thao tác cụ thể trên S3 (ví dụ: upload hoặc download) trong một khoảng thời gian giới hạn, **mà không cần có AWS credentials**.


Nói cách khác: Lambda tạo ra một "vé vào cửa có thời hạn" cho client. Client cầm vé đó upload trực tiếp lên S3, không cần đi qua Lambda nữa.


## Flow hoạt động


![Presigned URL Flow](/images/3-Blog/blog2_presigned_url.png)


Flow upload trong hệ thống của nhóm mình hoạt động như sau:


1. **Client gọi API** `POST /upload` qua API Gateway
2. **Lambda xử lý**: Xác thực user qua Cognito token, tạo một object key duy nhất (VD: `uploads/{userId}/{timestamp}_{filename}`), rồi dùng Boto3 gọi `generate_presigned_url()` để tạo Presigned PUT URL với thời hạn 5 phút
3. **Lambda trả URL** về cho client
4. **Client upload trực tiếp** lên S3 bằng HTTP PUT request với Presigned URL — file đi thẳng từ trình duyệt tới S3, không qua Lambda
5. **S3 Event Notification** kích hoạt khi file mới rơi vào bucket → đẩy message vào SQS → Step Functions điều phối phân tích


### Code Lambda tạo Presigned URL (Python)


```python
import boto3
import json
import uuid
from datetime import datetime


s3_client = boto3.client('s3')
BUCKET_NAME = 'malware-sandbox-raw-uploads'


def lambda_handler(event, context):
    # Lấy thông tin user từ Cognito
    user_id = event['requestContext']['authorizer']['claims']['sub']
    filename = json.loads(event['body'])['filename']
    
    # Tạo object key duy nhất
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    object_key = f"uploads/{user_id}/{timestamp}_{filename}"
    
    # Tạo Presigned URL (hết hạn sau 300 giây = 5 phút)
    presigned_url = s3_client.generate_presigned_url(
        'put_object',
        Params={
            'Bucket': BUCKET_NAME,
            'Key': object_key,
            'ContentType': 'application/octet-stream'
        },
        ExpiresIn=300
    )
    
    return {
        'statusCode': 200,
        'headers': {
            'Access-Control-Allow-Origin': '*'
        },
        'body': json.dumps({
            'upload_url': presigned_url,
            'object_key': object_key
        })
    }
```


### Code Client upload (JavaScript)


```javascript
// Bước 1: Gọi Lambda để lấy Presigned URL
const response = await fetch('https://api.example.com/upload', {
  method: 'POST',
  headers: {
    'Authorization': `Bearer ${cognitoToken}`,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({ filename: file.name })
});


const { upload_url } = await response.json();


// Bước 2: Upload trực tiếp lên S3
await fetch(upload_url, {
  method: 'PUT',
  headers: { 'Content-Type': 'application/octet-stream' },
  body: file  // File object từ input[type="file"]
});
```


## Những lỗi mình đã gặp (và cách fix)


### Lỗi 1: CORS — "No 'Access-Control-Allow-Origin' header"


Đây là lỗi đầu tiên mình gặp khi client gọi PUT lên S3. Trình duyệt chặn request vì S3 bucket chưa cấu hình CORS.


**Fix:** Vào S3 bucket → Permissions → CORS configuration:
```json
[
  {
    "AllowedHeaders": ["*"],
    "AllowedMethods": ["PUT", "GET"],
    "AllowedOrigins": ["https://your-domain.com"],
    "ExposeHeaders": ["ETag"],
    "MaxAgeSeconds": 3600
  }
]
```


### Lỗi 2: Content-Type không khớp


Khi tạo Presigned URL, mình set `ContentType: 'application/octet-stream'`. Nhưng phía client quên set header `Content-Type` hoặc set khác → S3 từ chối request với lỗi `403 SignatureDoesNotMatch`.


**Fix:** Content-Type trong Presigned URL params và trong request header của client **phải giống nhau y hệt**.


### Lỗi 3: URL hết hạn mà không hiểu tại sao


Mình set `ExpiresIn=60` (1 phút) để "an toàn". Kết quả: file lớn upload chậm trên mạng yếu → chưa xong đã hết hạn.


**Fix:** Tăng `ExpiresIn` lên 300 giây (5 phút) hoặc 900 giây (15 phút) cho file lớn. URL chỉ dùng được 1 lần nên không lo bị lạm dụng.


## So sánh: Upload qua Lambda vs Presigned URL


| Tiêu chí | Qua Lambda | Presigned URL |
|---|---|---|
| Giới hạn file size | 6MB (sync) / 10MB (API GW) | **5GB** (single PUT) |
| Chi phí compute | Tốn Lambda duration | **Gần như 0** (chỉ tốn 1 lần gọi tạo URL) |
| Tốc độ | Chậm (qua 2 lớp proxy) | **Nhanh** (upload thẳng S3) |
| Độ phức tạp | Đơn giản hơn ban đầu | Cần thêm bước tạo URL |
| Phù hợp | File nhỏ < 5MB | **File từ 1MB trở lên** |


## Bài học rút ra


1. **Đừng upload file binary qua Lambda** trừ khi file rất nhỏ (< 1MB) — vừa giới hạn size, vừa tốn tiền compute vô ích
2. **Presigned URL là best practice** của AWS cho file upload — hầu hết production system đều dùng
3. **CORS là bẫy lớn nhất** — nhớ cấu hình trước khi test từ trình duyệt
4. **Content-Type phải match** — đây là nguyên nhân #1 gây lỗi 403 khó hiểu
5. **Kết hợp S3 Event + SQS** để tạo flow bất đồng bộ hoàn chỉnh sau khi upload


---


📎 **Tham khảo thêm:**
- [AWS Documentation — Presigned URLs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html)
- [AWS Blog — Uploading to S3 directly from a web browser](https://aws.amazon.com/blogs/compute/uploading-to-amazon-s3-directly-from-a-web-or-mobile-application/)
