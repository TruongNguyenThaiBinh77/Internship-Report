---
title : "Thiết lập AWS Bedrock"
weight : 3 
chapter : false
pre : " <b> 5.3. </b> "
---

## Thiết lập AWS Bedrock & Knowledge Base

Trong phần này, bạn sẽ cấu hình AWS Bedrock để sử dụng Claude 3.5 Sonnet và tạo Knowledge Base cho việc truy xuất tài liệu.

### Bước 1: Kích hoạt Model Access

**QUAN TRỌNG:** Bạn phải kích hoạt quyền truy cập model trước khi sử dụng Bedrock, nếu không sẽ gặp lỗi `ValidationException`.

1. Vào **AWS Console → Services → Bedrock**
2. Ở thanh sidebar bên trái, click **Model access** (trong mục Foundation models)
3. Click nút **Manage model access** (màu cam)
4. Tìm và chọn các models sau:
   - ✅ **Anthropic - Claude 3.5 Sonnet v2** (`anthropic.claude-3-5-sonnet-20241022-v2:0`)
   - ✅ **Amazon - Titan Embeddings G1 - Text** (cho Knowledge Base)
5. Click **Request model access** (góc dưới bên phải)
6. Đợi phê duyệt:
   - **Instant access models**: Có sẵn ngay lập tức (màu xanh ✅)
   - **Models khác**: Đợi 5-30 phút (trạng thái đổi từ "In progress" → "Access granted")

![Kích hoạt Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-4.png)
![Kích hoạt Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-5.png)
![Kích hoạt Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-6.png)

**Kiểm tra models đã được kích hoạt:**
```bash
# Sử dụng AWS CLI
aws bedrock list-foundation-models --region us-west-2

# Hoặc kiểm tra trong Console:
# Bedrock → Model access → Status phải là "Access granted"
```

### Bước 2: Tạo S3 Bucket cho Knowledge Base

Knowledge Base yêu cầu S3 bucket để lưu trữ tài liệu.

1. Vào **S3 → Create bucket**
2. Tên bucket: `ev-rental-knowledge-docs` (phải là tên duy nhất toàn cầu)
3. Region: Giống với region Bedrock của bạn (ví dụ: `us-west-2`)
4. **Block all public access**: ✅ Bật (khuyến nghị)
5. Click **Create bucket**

![Tạo S3 Bucket](/images/5-Workshop/5.3-Setup-s3/image-7.png)
![Tạo S3 Bucket](/images/5-Workshop/5.3-Setup-s3/image-8.png)

### Bước 3: Upload tài liệu lên S3

Upload các tài liệu chính sách thuê xe (PDF, TXT, DOCX):

**Các tài liệu mẫu cần upload:**
- `rental-policy.pdf` - Chính sách và điều khoản thuê xe
- `pricing.pdf` - Thông tin giá xe
- `faq.txt` - Câu hỏi thường gặp
- `booking-process.pdf` - Cách đặt xe

**Upload qua Console:**
1. Vào S3 bucket của bạn: `ev-rental-knowledge-docs`
2. Click **Upload** → **Add files**
3. Chọn các tài liệu
4. Click **Upload**

**Upload qua AWS CLI:**
```bash
aws s3 cp rental-policy.pdf s3://ev-rental-knowledge-docs/
aws s3 cp pricing.pdf s3://ev-rental-knowledge-docs/
aws s3 cp faq.txt s3://ev-rental-knowledge-docs/
aws s3 cp booking-process.pdf s3://ev-rental-knowledge-docs/
```

### Bước 4: Tạo Knowledge Base

1. Vào **Bedrock → Knowledge Bases → Create**
2. **Knowledge base name**: `ev-rental-knowledge-base`
3. **Description**: "Chính sách và FAQ cho thuê xe điện VinFast"
4. Click **Next**

![Tạo Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-9.png)
![Tạo Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-10.png)

**Cấu hình Data source:**
1. **Data source name**: `rental-docs`
2. **S3 URI**: `s3://ev-rental-knowledge-docs/`
3. Click **Next**
![Tạo Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-11.png)

**Embeddings model:**
1. Chọn: **Titan Embeddings G1 - Text** (`amazon.titan-embed-text-v1`)
2. **Vector database**: Chọn **Bedrock managed (OpenSearch Serverless)** (tùy chọn dễ nhất)
3. Click **Next**
![Tạo Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-12.png)

**Review và tạo:**
1. Xem lại tất cả cài đặt
2. Click **Create knowledge base**
3. Đợi quá trình tạo hoàn tất (2-3 phút)

### Bước 5: Sync Data Source

Sau khi Knowledge Base được tạo, bạn cần đồng bộ dữ liệu:

1. Trong Knowledge Base, vào tab **Data sources**
2. Chọn data source của bạn: `rental-docs`
3. Click nút **Sync**
4. Đợi sync hoàn tất (kiểm tra trạng thái: "Syncing" → "Ready")
5. Quá trình này sẽ lập chỉ mục tất cả tài liệu và tạo vector embeddings

![Sync Data Source](/images/5-Workshop/5.3-Setup-Bedrock/image-6.png)

**Trạng thái Sync:**
- 🔄 **Syncing**: Đang xử lý
- ✅ **Ready**: Hoàn thành thành công
- ❌ **Failed**: Kiểm tra quyền S3 hoặc định dạng tài liệu

### Bước 6: Lấy Knowledge Base ID

Bạn sẽ cần ID này cho ứng dụng backend:

1. Trong trang Knowledge Base
2. Copy **Knowledge Base ID** (định dạng: `89CI1JSSE4` hoặc tương tự)
3. Lưu vào ghi chú - bạn sẽ sử dụng nó ở bước tiếp theo

**Ví dụ Knowledge Base ID:**
```
Knowledge Base ID: 89CI1JSSE4
Knowledge Base ARN: arn:aws:bedrock:us-west-2:123456789:knowledge-base/89CI1JSSE4
```

### Bước 7: Test Knowledge Base (Tùy chọn)

Test Knowledge Base trực tiếp trong console:

1. Vào Knowledge Base của bạn
2. Click tab **Test**
3. Nhập câu hỏi: "Chính sách thuê xe là gì?"
4. Click **Run**
5. Xác minh nó trả về thông tin liên quan từ tài liệu

### Checklist xác minh

Trước khi chuyển sang bước tiếp theo, đảm bảo:

- ✅ Quyền truy cập Claude 3.5 Sonnet v2 đã được **cấp**
- ✅ Quyền truy cập Titan Embeddings đã được **cấp**
- ✅ S3 bucket đã tạo và upload tài liệu
- ✅ Knowledge Base đã tạo và sync thành công
- ✅ Knowledge Base ID đã lưu
- ✅ Câu hỏi test trả về kết quả liên quan

### Xử lý sự cố

**Vấn đề: "ValidationException: Model not enabled"**
- Giải pháp: Vào Bedrock → Model access và kích hoạt model

**Vấn đề: "Sync failed"**
- Kiểm tra quyền truy cập S3 bucket
- Xác minh định dạng tài liệu (hỗ trợ PDF, TXT, DOCX)
- Kiểm tra CloudWatch Logs để xem lỗi chi tiết

**Vấn đề: "Không có kết quả từ Knowledge Base"**
- Đảm bảo tài liệu đã upload lên S3
- Chạy sync lại
- Đợi vài phút sau khi sync hoàn tất
- Thử đặt câu hỏi theo cách khác

---

**Tiếp theo:** Chuyển sang [Deploy Backend API](../5.4-Deploy-Backend/) để xây dựng FastAPI server.
