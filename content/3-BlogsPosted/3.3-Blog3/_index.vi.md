---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

# AWS CONFIG AUTO-REMEDIATION — TỰ ĐỘNG KHÓA S3 BUCKET TRONG 1 GIÂY KHI AI ĐÓ LỠ MỞ PUBLIC


## Câu chuyện bắt đầu từ một sai lầm


Mình luôn nghĩ rằng chuyện "lỡ tay bật Public Access cho S3 bucket" chỉ xảy ra trong tutorial, không ai làm vậy trong thực tế. Cho đến khi chính mình test CORS cho hệ thống upload file, vào S3 console bỏ tick **Block Public Access** để debug... rồi quên bật lại.


May mắn là lúc đó bucket chưa có dữ liệu thật. Nhưng trong hệ thống phân tích mã độc của nhóm mình, S3 bucket chứa các file nghi ngờ là malware — nếu bị public, hậu quả sẽ cực kỳ nghiêm trọng. Từ đó mình quyết định: **phải có cơ chế tự động khóa lại ngay lập tức, không phụ thuộc vào con người**.


Giải pháp mình chọn là bộ ba: **AWS Config + EventBridge + Lambda**.


## AWS Config là gì?


AWS Config là dịch vụ giám sát cấu hình tài nguyên trên AWS. Nó liên tục theo dõi và đánh giá xem các tài nguyên của bạn có tuân thủ các "luật" (rules) mà bạn đặt ra hay không.


Ví dụ: bạn có thể đặt luật **"Tất cả S3 bucket phải Block Public Access"**. Mỗi khi có ai thay đổi cấu hình S3, Config sẽ đánh giá lại và đánh dấu bucket đó là **COMPLIANT** (tuân thủ) hoặc **NON_COMPLIANT** (vi phạm).


Nhưng Config chỉ **phát hiện** — nó không tự sửa. Để tự động sửa lỗi, mình cần thêm EventBridge và Lambda.


## Kiến trúc Auto-Remediation


![Auto-Remediation Architecture](/images/3-Blog/blog3_auto_remediation.png)


Flow hoạt động:


1. **Ai đó bật Public Access** trên S3 bucket (vô tình hoặc cố ý)
2. **AWS Config** phát hiện thay đổi và đánh giá bucket là **NON_COMPLIANT** theo rule `s3-bucket-public-read-prohibited`
3. **EventBridge Rule** bắt sự kiện compliance change từ Config
4. **Lambda function** được kích hoạt, gọi API `PutPublicAccessBlock` để khóa lại bucket ngay lập tức
5. **S3 bucket** trở lại trạng thái an toàn — toàn bộ quá trình diễn ra trong **chưa đầy 1 giây**


## Cài đặt từng bước


### Bước 1: Tạo AWS Config Rule


Vào AWS Config → Rules → Add rule → chọn **Managed rule**:
- Rule name: `s3-bucket-public-read-prohibited`
- Trigger: Configuration changes
- Scope: Resources — `AWS::S3::Bucket`


Rule này sẽ tự động đánh giá mỗi khi có thay đổi cấu hình trên bất kỳ S3 bucket nào.


### Bước 2: Tạo Lambda function xử lý remediation


```python
import boto3
import json


s3_client = boto3.client('s3')


def lambda_handler(event, context):
    """
    Auto-remediation: Khi nhận event từ EventBridge báo S3 bucket 
    bị NON_COMPLIANT, tự động Block Public Access.
    """
    detail = event.get('detail', {})
    
    # Lấy tên bucket từ event
    resource_id = detail.get('resourceId', '')
    compliance = detail.get('newEvaluationResult', {}).get('complianceType', '')
    
    if compliance != 'NON_COMPLIANT':
        print(f"Bucket {resource_id} is compliant. No action needed.")
        return
    
    print(f"⚠️ Bucket {resource_id} is NON_COMPLIANT! Remediating...")
    
    try:
        # Khóa Public Access ngay lập tức
        s3_client.put_public_access_block(
            Bucket=resource_id,
            PublicAccessBlockConfiguration={
                'BlockPublicAcls': True,
                'IgnorePublicAcls': True,
                'BlockPublicPolicy': True,
                'RestrictPublicBuckets': True
            }
        )
        print(f"✅ Successfully blocked public access for bucket: {resource_id}")
        
    except Exception as e:
        print(f"❌ Failed to remediate bucket {resource_id}: {str(e)}")
        raise e
```


IAM Role cho Lambda cần có permission:
```json
{
  "Effect": "Allow",
  "Action": [
    "s3:PutBucketPublicAccessBlock",
    "s3:GetBucketPublicAccessBlock"
  ],
  "Resource": "arn:aws:s3:::*"
}
```


### Bước 3: Tạo EventBridge Rule


Vào EventBridge → Create rule:
- **Event pattern:**
```json
{
  "source": ["aws.config"],
  "detail-type": ["Config Rules Compliance Change"],
  "detail": {
    "messageType": ["ComplianceChangeNotification"],
    "configRuleName": ["s3-bucket-public-read-prohibited"],
    "newEvaluationResult": {
      "complianceType": ["NON_COMPLIANT"]
    }
  }
}
```
- **Target:** Lambda function ở Bước 2


### Bước 4: Test thử


1. Vào S3 bucket bất kỳ → Permissions → tắt Block Public Access
2. Đợi khoảng 30-60 giây (thời gian Config đánh giá)
3. Kiểm tra lại → Block Public Access đã tự động được bật lại ✅
4. Vào CloudWatch Logs của Lambda → thấy log `"Successfully blocked public access"`


## So sánh: Thủ công vs Tự động


| Tiêu chí | Xử lý thủ công | Auto-Remediation |
|---|---|---|
| Thời gian phát hiện | Hàng giờ đến hàng ngày | **< 1 phút** |
| Thời gian khắc phục | Phụ thuộc con người | **< 1 giây** (sau khi phát hiện) |
| Độ tin cậy | Dễ quên, dễ bỏ sót | **100% tự động** |
| Hoạt động ngoài giờ | Không (trừ khi có người trực) | **24/7** |
| Chi phí | Thời gian nhân sự | ~$1/tháng (Config rule) |


## Mở rộng thêm


Ngoài S3 Public Access, mình còn áp dụng pattern tương tự cho:


- **Security Group mở port 22 ra 0.0.0.0/0** → tự động xóa rule
- **EBS volume không được mã hóa** → tự động tạo snapshot mã hóa
- **IAM Access Key quá 90 ngày** → tự động gửi cảnh báo qua SNS


Tất cả đều dùng chung kiến trúc: **Config Rule → EventBridge → Lambda**.


## Bài học rút ra


1. **Con người sẽ luôn mắc sai lầm** — đừng phụ thuộc vào checklist thủ công cho bảo mật
2. **AWS Config + EventBridge + Lambda** là bộ ba vàng cho auto-remediation
3. **Chi phí rất thấp** — khoảng $1-2/tháng cho vài Config rules, đổi lại sự an tâm tuyệt đối
4. **Nên log mọi thứ** — ghi lại ai đã thay đổi gì, Lambda đã fix gì, để phục vụ audit sau này
5. **Test trước khi tin tưởng** — luôn thử break rule rồi xem Lambda có tự fix không


Đây có lẽ là một trong những thứ mình tự hào nhất trong dự án thực tập. Không phải vì nó phức tạp, mà vì nó giải quyết được một vấn đề thực tế mà nhiều team lớn vẫn đang gặp: **human error trong cấu hình bảo mật đám mây**.


---


📎 **Tham khảo thêm:**
- [AWS Documentation — AWS Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html)
- [AWS Documentation — Remediating Noncompliant Resources](https://docs.aws.amazon.com/config/latest/developerguide/remediation.html)
- [AWS Blog — Auto-Remediate Non-Compliant AWS Resources](https://aws.amazon.com/blogs/mt/auto-remediate-non-compliant-aws-resources/)
