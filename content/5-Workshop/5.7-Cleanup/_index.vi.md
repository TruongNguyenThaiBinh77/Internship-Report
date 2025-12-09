---
title : "Dọn dẹp Tài nguyên"
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## Dọn dẹp Tài nguyên

Sau khi hoàn thành workshop, hãy làm theo các bước sau để dọn dẹp tất cả tài nguyên và tránh phí AWS không cần thiết.

### Tại sao Dọn dẹp là Quan trọng

- **Tiết kiệm Chi phí:** AWS tính phí cho các tài nguyên đang hoạt động như Bedrock Knowledge Bases, S3 storage và các dịch vụ đang chạy
- **Bảo mật:** Xóa các credentials IAM không sử dụng để duy trì best practices về bảo mật
- **Tổ chức:** Giữ tài khoản AWS của bạn sạch sẽ và có tổ chức

---

## Bước 1: Xóa AWS Bedrock Knowledge Base

### 1.1 Xóa Knowledge Base

1. Mở **AWS Bedrock Console**
2. Điều hướng đến **Knowledge Bases** ở thanh bên trái
3. Chọn Knowledge Base của bạn: `ev-rental-knowledge-base`
4. Click **Delete**
5. Xác nhận xóa bằng cách nhập tên Knowledge Base
6. Click **Delete** để xác nhận

⚠️ **Lưu ý:** Điều này cũng sẽ xóa các kết nối data source liên quan.

### 1.2 Xóa S3 Bucket và Documents

1. Mở **S3 Console**
2. Tìm bucket của bạn: `ev-rental-knowledge-docs`
3. Chọn bucket
4. Click **Empty** để xóa tất cả objects
5. Xác nhận bằng cách nhập "permanently delete"
6. Sau khi làm trống, click **Delete** trên bucket
7. Xác nhận bằng cách nhập tên bucket

**Hoặc dùng AWS CLI:**
```bash
# Xóa tất cả objects trong bucket
aws s3 rm s3://ev-rental-knowledge-docs --recursive

# Xóa bucket
aws s3 rb s3://ev-rental-knowledge-docs
```

---

## Bước 2: Xóa IAM User và Access Keys

### 2.1 Xóa Access Keys

1. Mở **IAM Console**
2. Điều hướng đến **Users**
3. Chọn user của bạn (ví dụ: `bedrock-agent-user`)
4. Click vào tab **Security credentials**
5. Dưới **Access keys**, tìm access key của bạn
6. Click **Delete** bên cạnh access key
7. Xác nhận xóa

### 2.2 Xóa IAM User (Tùy chọn)

Nếu bạn đã tạo IAM user riêng cho workshop này:

1. Trong IAM Console, chọn user
2. Click **Delete user**
3. Xác nhận bằng cách check vào ô
4. Click **Delete**

**Hoặc dùng AWS CLI:**
```bash
# Liệt kê access keys
aws iam list-access-keys --user-name bedrock-agent-user

# Xóa access key (thay bằng key ID của bạn)
aws iam delete-access-key --user-name bedrock-agent-user --access-key-id AKIA5GPEMGJZK6E7PMEB

# Xóa user
aws iam delete-user --user-name bedrock-agent-user
```

---

## Bước 3: Dừng Các Dịch vụ Local

### 3.1 Dừng FastAPI Backend

Trong terminal nơi FastAPI đang chạy:

1. Nhấn `Ctrl + C` để dừng server
2. Deactivate virtual environment:
   ```bash
   deactivate
   ```

3. Tùy chọn xóa thư mục dự án:
   ```bash
   # Trên macOS/Linux
   rm -rf ev-rental-backend
   
   # Trên Windows
   rmdir /s ev-rental-backend
   ```

### 3.2 Dừng React Frontend

Trong terminal nơi React đang chạy:

1. Nhấn `Ctrl + C` để dừng development server

2. Tùy chọn xóa thư mục dự án:
   ```bash
   # Trên macOS/Linux
   rm -rf ev-rental-frontend
   
   # Trên Windows
   rmdir /s ev-rental-frontend
   ```

### 3.3 Dừng PostgreSQL Database

Nếu bạn đã cài PostgreSQL local cho workshop này:

**Trên macOS:**
```bash
# Dừng PostgreSQL service
brew services stop postgresql@14
```

**Trên Linux:**
```bash
sudo systemctl stop postgresql
```

**Trên Windows:**
```bash
# Mở Services (services.msc)
# Tìm service "PostgreSQL"
# Right-click → Stop
```

### 3.4 Xóa Database (Tùy chọn)

Nếu bạn muốn xóa hoàn toàn database:

```bash
# Kết nối PostgreSQL
psql -U postgres

# Xóa database
DROP DATABASE ev_rental_db;

# Thoát
\q
```

---

## Bước 4: Xóa Các File Environment

Xóa các file `.env` nhạy cảm chứa credentials:

**Backend:**
```bash
cd ev-rental-backend
rm .env
```

**Frontend:**
```bash
cd ev-rental-frontend
rm .env
```

⚠️ **Lưu ý Bảo mật:** Không bao giờ commit file `.env` vào Git. Luôn thêm chúng vào `.gitignore`.

---

## Bước 5: Xác minh Dọn dẹp

### 5.1 Kiểm tra Tài nguyên AWS

Xác minh tất cả tài nguyên đã được xóa:

1. **Bedrock Console:**
   - Không có Knowledge Bases nào được liệt kê
   - Không có model invocations đang hoạt động

2. **S3 Console:**
   - Bucket `ev-rental-knowledge-docs` đã bị xóa

3. **IAM Console:**
   - Access keys đã bị xóa
   - IAM user đã bị xóa (nếu bạn chọn xóa)

### 5.2 Kiểm tra Chi phí AWS

1. Mở **AWS Billing Console**
2. Kiểm tra **Bills** cho tháng hiện tại
3. Xác minh các khoản phí:
   - Phí Bedrock sẽ dừng sau khi xóa Knowledge Base
   - Phí S3 storage sẽ dừng sau khi xóa bucket
   - Không có phí compute đang chạy

**Hoặc dùng AWS CLI:**
```bash
aws ce get-cost-and-usage \
  --time-period Start=2024-12-01,End=2024-12-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=SERVICE
```

---

## Chi tiết Chi phí

Đây là những gì bạn có thể đã bị tính phí trong workshop:

| Dịch vụ | Chi phí Ước tính | Ghi chú |
|---------|------------------|---------|
| **AWS Bedrock - Claude 3.5 Sonnet** | ~$0.50 - $2.00 | Phụ thuộc số lượng truy vấn |
| **AWS Bedrock - Knowledge Base** | ~$0.10 - $0.50 | Vector storage và retrieval |
| **S3 Storage** | ~$0.02 | Tối thiểu cho documents nhỏ |
| **Data Transfer** | ~$0.05 | Thường trong free tier |
| **Tổng** | ~$0.67 - $2.57 | Ước tính cho workshop |

⚠️ **Lưu ý:** Hầu hết chi phí đến từ các API calls Bedrock. Càng test lâu, chi phí càng cao.

---

## Danh sách Kiểm tra Dọn dẹp

Trước khi kết thúc, xác minh tất cả mục đã hoàn thành:

### Tài nguyên AWS
- ✅ Bedrock Knowledge Base đã xóa
- ✅ S3 bucket đã làm trống và xóa
- ✅ IAM Access Keys đã xóa
- ✅ IAM User đã xóa (tùy chọn)

### Tài nguyên Local
- ✅ FastAPI backend đã dừng
- ✅ React frontend đã dừng
- ✅ PostgreSQL database đã dừng
- ✅ PostgreSQL database đã xóa (tùy chọn)

### File Nhạy cảm
- ✅ File `.env` backend đã xóa
- ✅ File `.env` frontend đã xóa
- ✅ Không có AWS credentials trong các file dự án

### Xác minh
- ✅ AWS Console không hiển thị tài nguyên đang hoạt động
- ✅ Billing dashboard hiển thị phí đã dừng
- ✅ Các dịch vụ local không chạy

---

## Xử lý Sự cố Dọn dẹp

**Vấn đề: Không thể xóa S3 bucket - "Bucket not empty"**
- Giải pháp: Làm trống tất cả objects trước bằng S3 Console hoặc CLI
- Lệnh: `aws s3 rm s3://bucket-name --recursive`

**Vấn đề: Không thể xóa Knowledge Base - "In use"**
- Giải pháp: Đợi vài phút để các thao tác đang chờ hoàn thành
- Kiểm tra xem có API calls nào vẫn đang tham chiếu đến nó

**Vấn đề: Xóa IAM User thất bại - "User has attached policies"**
- Giải pháp: Detach tất cả policies trước
- Vào IAM → Users → Chọn user → Permissions → Detach policies

**Vấn đề: PostgreSQL không dừng**
- Giải pháp: Force kill process
- Trên macOS/Linux: `sudo killall postgres`
- Trên Windows: Dùng Task Manager để end các processes PostgreSQL

---

## Tùy chọn: Tiếp tục Học

Nếu bạn muốn tiếp tục thử nghiệm:

### Giữ lại Các Tài nguyên:
- ✅ IAM User (với permissions tối thiểu)
- ✅ Bedrock model access (không tính phí khi không sử dụng)

### Những gì Bạn Có thể Làm Tiếp:
- Thêm nhiều documents vào Knowledge Base
- Triển khai thêm agent tools
- Deploy lên AWS Lambda cho serverless operation
- Thêm authentication và user management
- Tích hợp với hệ thống đặt xe thực

---

## Kết luận

🎉 **Chúc mừng!** Bạn đã thành công:

1. ✅ Xây dựng AI Agent sử dụng AWS Bedrock và Claude 3.5 Sonnet
2. ✅ Tích hợp Knowledge Bases cho việc truy xuất tài liệu thông minh
3. ✅ Tạo FastAPI backend với Strands Agent SDK
4. ✅ Phát triển React frontend cho tương tác người dùng
5. ✅ Kiểm thử tất cả tính năng end-to-end
6. ✅ Dọn dẹp tài nguyên để tránh phí

### Những Điều Chính:

- **AI Agents** có thể tự động chọn tools và đưa ra quyết định
- **AWS Bedrock** đơn giản hóa truy cập đến các foundation models như Claude
- **Knowledge Bases** cho phép semantic search trên documents
- **Strands SDK** cung cấp framework cho xây dựng agent workflows
- **FastAPI + React** tạo ứng dụng AI full-stack hiện đại

### Các Bước Tiếp theo:

- Khám phá các Bedrock models khác (Llama 3, Mistral, v.v.)
- Học về RAG (Retrieval Augmented Generation)
- Xây dựng agent workflows phức tạp hơn
- Deploy lên production sử dụng các dịch vụ AWS

---

