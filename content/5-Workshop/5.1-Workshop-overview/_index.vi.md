---
title : "Tổng quan Workshop"
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

## Giới thiệu về EV Rental AI Agent

### AI Agent là gì?

**AI Agent** là một hệ thống thông minh có thể:
- Hiểu các câu hỏi bằng ngôn ngữ tự nhiên
- Tự động chọn và thực thi các công cụ/chức năng phù hợp
- Đưa ra quyết định dựa trên ngữ cảnh
- Cung cấp phản hồi có cấu trúc kèm dữ liệu

Khác với chatbot truyền thống có câu trả lời cố định, AI Agent có thể **suy luận** và **hành động** một cách linh hoạt.

### Kiến trúc hệ thống

EV Rental AI Agent sử dụng **kiến trúc đa tầng**:

```
┌─────────────────┐
│  Giao diện      │  ← React Frontend (Chat UI)
└────────┬────────┘
         │ HTTP/REST
         ↓
┌─────────────────┐
│  FastAPI Server │  ← Backend điều phối
└────────┬────────┘
         │
    ┌────┴────────────────┐
    ↓                     ↓
┌──────────┐      ┌──────────────┐
│ Strands  │      │  PostgreSQL  │
│ Agent SDK│      │  (Lịch sử)   │
└────┬─────┘      └──────────────┘
     │
     ├─────→ AWS Bedrock (Claude 3.5 Sonnet)
     ├─────→ Knowledge Base (Chính sách/FAQ)
     └─────→ Backend API (Xe/Trạm sạc)
```


### Các thành phần chính

| Thành phần | Công nghệ | Vai trò |
|-----------|-----------|---------|
| **AI Model** | AWS Bedrock - Claude 3.5 Sonnet | Xử lý ngôn ngữ tự nhiên & sinh phản hồi |
| **Agent Framework** | Strands Agent SDK | Tự động chọn tool & điều phối |
| **Backend API** | FastAPI (Python) | REST API server cho logic agent |
| **Cơ sở dữ liệu** | PostgreSQL | Lưu trữ lịch sử chat & phiên |
| **Frontend** | React + Chakra UI | Giao diện chat tương tác |
| **Knowledge Base** | AWS Bedrock KB | Truy xuất tài liệu (chính sách, FAQ) |

### Các tính năng chính

#### 1. **Tìm kiếm Knowledge Base**
Agent tìm kiếm trong tài liệu đã upload để trả lời câu hỏi về:
- Chính sách thuê xe
- Thông tin giá cả
- Quy trình đặt xe
- Điều khoản và điều kiện

**Ví dụ câu hỏi:** 
> "Chính sách thuê xe của bạn là gì?"

**Phản hồi của Agent:**
```markdown
## 📋 Chính sách thuê xe VinFast

### 📄 Giấy tờ cần thiết:
- ✅ CMND/CCCD còn hiệu lực
- ✅ Bằng lái xe (Hạng B1 trở lên)
- ✅ Chứng minh nơi cư trú

### 💰 Giá thuê:
- **VF8**: 1,500,000 VNĐ/ngày
- **VF9**: 2,000,000 VNĐ/ngày
- **Đặt cọc**: 10,000,000 VNĐ
```

#### 2. **Tìm kiếm xe**
Agent truy vấn backend API để tìm xe available dựa trên:
- Địa điểm (thành phố)
- Khoảng thời gian
- Mẫu/loại xe

**Định dạng phản hồi:** Card xe tương tác với thông số kỹ thuật

#### 3. **Tìm trạm sạc**
Agent lấy thông tin trạm sạc gần đó với:
- Địa chỉ và trạng thái
- Số trạm sạc khả dụng
- Khoảng cách (nếu có vị trí)

**Định dạng phản hồi:** Card trạm sạc với tình trạng thời gian thực

### Mục tiêu Workshop

Sau khi hoàn thành workshop, bạn sẽ có thể:

1. ✅ **Cấu hình AWS Bedrock** - Kích hoạt Claude models và tạo Knowledge Base
2. ✅ **Xây dựng Backend AI Agent** - Sử dụng Strands SDK để điều phối nhiều tools
3. ✅ **Triển khai giao diện Chat** - Tạo React chat UI responsive
4. ✅ **Kiểm thử End-to-End** - Tương tác với AI agent và xác minh tất cả chức năng

### Công nghệ sử dụng

**AWS Services:**
- AWS Bedrock (Claude 3.5 Sonnet v2)
- AWS Bedrock Knowledge Bases
- AWS S3 (lưu trữ tài liệu)
- IAM (quản lý truy cập)

**Backend:**
- Python 3.11+
- FastAPI
- Strands Agent SDK
- PostgreSQL
- SQLAlchemy

**Frontend:**
- React 18
- Chakra UI
- Axios
- React Markdown

### Luồng Workshop

```
Bước 1: Yêu cầu chuẩn bị
   ↓
Bước 2: Thiết lập AWS Bedrock & Knowledge Base
   ↓
Bước 3: Triển khai Backend API (FastAPI)
   ↓
Bước 4: Triển khai Frontend (React)
   ↓
Bước 5: Kiểm thử AI Agent
   ↓
Bước 6: Dọn dẹp tài nguyên
```

---

**Tiếp theo:** Chuyển sang [Yêu cầu chuẩn bị](../5.2-Prerequiste/) để chuẩn bị môi trường.
