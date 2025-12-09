---
title : "Điều kiện tiên quyết"
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

## Điều kiện tiên quyết cho Workshop EV Rental AI Agent

Trước khi bắt đầu workshop này, hãy đảm bảo bạn đã chuẩn bị các yêu cầu sau:

### 1. Tài khoản AWS

Bạn cần một **Tài khoản AWS** với quyền phù hợp để:
- Truy cập dịch vụ AWS Bedrock
- Tạo và quản lý IAM users
- Tạo S3 buckets (cho Knowledge Base)
- Tạo Knowledge Bases

**Lưu ý:** Bedrock chỉ khả dụng ở một số vùng cụ thể. Các vùng được khuyến nghị:
- `us-west-2` (Oregon)
- `us-east-1` (N. Virginia)
- `ap-southeast-1` (Singapore)


### 2. IAM User với Quyền Bedrock

Bạn cần tạo IAM User với quyền truy cập AWS Bedrock cho ứng dụng.

**Bước 1: Tạo IAM User**
1. Vào **AWS Console → IAM → Users → Create User**

![AWS](/images/5-Workshop/5.2-Prerequiste/image.png)

![AWS](/images/5-Workshop/5.2-Prerequiste/image-1.png)

2. Tên user: `bedrock-agent-user`
3. ✅ Chọn: **Provide user access to the AWS Management Console** (tùy chọn)
4. ✅ Chọn: **I want to create an IAM user**
5. Click **Next**

**Bước 2: Gán Quyền**
1. Chọn: **Attach policies directly**
2. Tìm và chọn các policies sau:
   - ✅ `AmazonBedrockFullAccess` - Quyền truy cập đầy đủ Bedrock models và Knowledge Bases
   - ✅ (Tùy chọn) `AmazonS3ReadOnlyAccess` - Nếu sử dụng Knowledge Base với S3
3. Click **Next** → **Create User**

![AWS](/images/5-Workshop/5.2-Prerequiste/image-2.png)

**Bước 3: Tạo Access Keys**
1. Click vào user vừa tạo: `bedrock-agent-user`
2. Vào tab **Security credentials**
3. Cuộn xuống **Access keys** → Click **Create access key**
6. ⚠️ **QUAN TRỌNG**: Copy và lưu lại:
   - `Access Key ID` (ví dụ: `AKIAIOSFODNN7EXAMPLE`)
   - `Secret Access Key` (chỉ hiển thị 1 lần, ví dụ: `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`)
7. Click **Done**

![AWS](/images/5-Workshop/5.2-Prerequiste/image-3.png)

⚠️ **Lưu ý Bảo mật:**
```bash
# Lưu vào file .env (KHÔNG commit lên Git)
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID_HERE
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY_HERE
AWS_REGION=us-west-2
```

### 3. Môi trường Phát triển

#### 3.1. Môi trường Python
- **Python 3.11 hoặc cao hơn**
- Trình quản lý package: `pip`

**Kiểm tra cài đặt:**
```bash
python --version
# Mong đợi: Python 3.11.x hoặc cao hơn

pip --version
```

#### 3.2. Môi trường Node.js
- **Node.js 18+ và npm**
- Yêu cầu cho React frontend

**Kiểm tra cài đặt:**
```bash
node --version
# Mong đợi: v18.x.x hoặc cao hơn

npm --version
```

#### 3.3. Cơ sở dữ liệu PostgreSQL
- **PostgreSQL 14+ cài đặt local** hoặc sử dụng Docker

**Tùy chọn 1: Cài đặt local**
- Tải từ: https://www.postgresql.org/download/
- Tạo database: `ev_rental_db`

**Tùy chọn 2: Sử dụng Docker**
```bash
docker run -d \
  --name postgres-ev \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=ev_rental_db \
  -p 5432:5432 \
  postgres:14
```

**Kiểm tra PostgreSQL:**
```bash
# Kiểm tra PostgreSQL đang chạy
psql --version

# Kết nối database
psql -U postgres -d ev_rental_db
```

### 4. Code Editor & Công cụ

- **VS Code** hoặc IDE bạn ưa thích
- **Git** để clone repositories
- **Postman** hoặc **cURL** để test API (tùy chọn)

**Cài đặt VS Code:**
- Tải từ: https://code.visualstudio.com/

**Cài đặt Git:**
```bash
# macOS
brew install git

# Windows
# Tải từ: https://git-scm.com/download/win

# Kiểm tra
git --version
```

### 5. AWS CLI (Tùy chọn)

Cài đặt AWS CLI để tương tác với các dịch vụ AWS từ command line:

```bash
# macOS/Linux
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

# Windows
# Tải từ: https://awscli.amazonaws.com/AWSCLIV2.msi

# Kiểm tra
aws --version
```

**Cấu hình AWS CLI:**
```bash
aws configure
# Nhập Access Key ID: AKIA5GPEMGJZK6E7PMEB
# Nhập Secret Access Key: (dán secret key của bạn)
# Default region name: us-west-2
# Default output format: json
```

**Test AWS CLI:**
```bash
# Liệt kê các Bedrock models có sẵn
aws bedrock list-foundation-models --region us-west-2

# Kiểm tra identity của bạn
aws sts get-caller-identity
```

### Danh sách Kiểm tra

Trước khi tiếp tục bước tiếp theo, đảm bảo bạn có:

- ✅ Tài khoản AWS với quyền truy cập Bedrock ở vùng được hỗ trợ
- ✅ IAM User đã tạo với policy `AmazonBedrockFullAccess`
- ✅ Access Key ID và Secret Access Key đã lưu an toàn
- ✅ Python 3.11+ đã cài đặt và kiểm tra
- ✅ Node.js 18+ và npm đã cài đặt và kiểm tra
- ✅ PostgreSQL 14+ database đang chạy
- ✅ Code editor (VS Code khuyến nghị) đã cài đặt
- ✅ Git đã cài đặt và cấu hình
- ✅ (Tùy chọn) AWS CLI đã cài đặt và cấu hình

### Chi phí Ước tính

Workshop này sử dụng các dịch vụ AWS sau:

| Dịch vụ | Chi phí Ước tính | Ghi chú |
|---------|------------------|---------|
| **AWS Bedrock - Claude 3.5 Sonnet** | ~$0.50 - $2.00 | Tính theo API call (input/output tokens) |
| **AWS Bedrock - Knowledge Base** | ~$0.10 - $0.50 | Vector storage + retrieval |
| **S3 Storage** | ~$0.02 | Tối thiểu cho documents |
| **Data Transfer** | ~$0.05 | Thường trong free tier |
| **Tổng** | ~$0.67 - $2.57 | Cho toàn bộ workshop |

💡 **Lưu ý:** Nhớ dọn dẹp tài nguyên sau workshop để tránh phí phát sinh!

---

**Tiếp theo:** Chuyển sang [Thiết lập AWS Bedrock](../5.3-Setup-Bedrock/) để enable models và tạo Knowledge Base.