---
title : "Kiểm thử Hệ thống"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Kiểm thử EV Rental AI Agent

Trong phần này, bạn sẽ kiểm thử cả ba tính năng cốt lõi của AI Agent để đảm bảo mọi thứ hoạt động chính xác.

### Điều kiện Trước khi Kiểm thử

Trước khi kiểm thử, đảm bảo:
- ✅ Backend server đang chạy tại `http://localhost:8000`
- ✅ Frontend application đang chạy tại `http://localhost:3000`
- ✅ Cơ sở dữ liệu PostgreSQL đang chạy và có dữ liệu test
- ✅ AWS Bedrock Knowledge Base đã được đồng bộ và sẵn sàng

### Kịch bản Kiểm thử 1: Tìm kiếm Knowledge Base

AI Agent phải có khả năng trả lời câu hỏi về chính sách thuê xe, giá cả và FAQ sử dụng Knowledge Base.

**Câu hỏi Kiểm thử:**

1. **Chính sách Thuê xe:**
   ```
   User: "Chính sách thuê xe là gì?"
   Kết quả mong đợi: Agent trả về chi tiết chính sách từ Knowledge Base
   ```

2. **Giấy tờ Yêu cầu:**
   ```
   User: "Tôi cần giấy tờ gì để thuê xe?"
   Kết quả mong đợi: Agent liệt kê giấy tờ cần thiết (CMND, bằng lái, tiền cọc)
   ```

3. **Thông tin Giá cả:**
   ```
   User: "Giá thuê xe VinFast VF8 là bao nhiêu?"
   Kết quả mong đợi: Agent cung cấp chi tiết giá từ Knowledge Base
   ```

4. **Quy trình Đặt xe:**
   ```
   User: "Làm thế nào để đặt xe?"
   Kết quả mong đợi: Agent giải thích quy trình đặt xe từng bước
   ```

**Xác minh:**
- ✅ Phản hồi bao gồm trích dẫn từ Knowledge Base
- ✅ Câu trả lời liên quan và chính xác
- ✅ Định dạng Markdown hiển thị đúng
- ✅ Thời gian phản hồi dưới 5 giây

![Kiểm thử Tìm kiếm Knowledge Base](/images/5-Workshop/5.6-Testing/image-12.png)

### Kịch bản Kiểm thử 2: Tìm kiếm Xe

AI Agent phải tìm kiếm cơ sở dữ liệu PostgreSQL để tìm xe có sẵn theo địa điểm và ngày tháng.

**Câu hỏi Kiểm thử:**

1. **Tìm theo Địa điểm:**
   ```
   User: "Tìm xe ở Hà Nội"
   Kết quả mong đợi: Agent liệt kê xe có sẵn ở Hà Nội
   ```

2. **Tìm theo Model:**
   ```
   User: "Có xe VinFast VF8 nào available không?"
   Kết quả mong đợi: Agent hiển thị xe VF8 với trạng thái sẵn có
   ```

3. **Tìm theo Khoảng Ngày:**
   ```
   User: "Tìm xe VF9 ở Hồ Chí Minh từ ngày 20/12 đến 25/12"
   Kết quả mong đợi: Agent tìm xe sẵn có trong khoảng ngày đó
   ```

4. **Tìm theo Khoảng Giá:**
   ```
   User: "Xe nào dưới 1 triệu đồng/ngày?"
   Kết quả mong đợi: Agent lọc xe theo giá
   ```

**Xác minh:**
- ✅ Agent trích xuất đúng tham số tìm kiếm (địa điểm, model, ngày)
- ✅ Kết quả bao gồm chi tiết xe (model, giá, địa điểm, trạng thái)
- ✅ Dữ liệu được lấy từ cơ sở dữ liệu PostgreSQL
- ✅ Kết quả được định dạng thành bảng hoặc danh sách dễ đọc

**Định dạng Phản hồi Mong đợi:**
```markdown
## 🚗 Xe Có Sẵn

| Model | Địa điểm | Giá/Ngày | Trạng thái |
|-------|----------|----------|------------|
| VinFast VF8 | Hà Nội | 800,000đ | Có sẵn |
| VinFast VF9 | Hà Nội | 1,200,000đ | Có sẵn |
```

### Kịch bản Kiểm thử 3: Tìm Trạm Sạc

AI Agent phải tìm trạm sạc gần đó với thông tin sẵn có theo thời gian thực.

**Câu hỏi Kiểm thử:**

1. **Tìm theo Quận:**
   ```
   User: "Trạm sạc gần Quận Hoàn Kiếm"
   Kết quả mong đợi: Agent liệt kê trạm sạc ở quận Hoàn Kiếm
   ```

2. **Tìm theo Địa chỉ:**
   ```
   User: "Tìm trạm sạc ở Quận 1, TP.HCM"
   Kết quả mong đợi: Agent tìm trạm ở Quận 1, TP.HCM
   ```

3. **Kiểm tra Trạng thái Trạm:**
   ```
   User: "Trạm sạc nào còn trống?"
   Kết quả mong đợi: Agent hiển thị trạm có cổng sạc còn trống
   ```

4. **Lọc theo Loại Connector:**
   ```
   User: "Trạm sạc có CCS2 connector"
   Kết quả mong đợi: Agent lọc trạm có connector CCS2
   ```

**Xác minh:**
- ✅ Agent nhận diện đúng địa điểm từ câu hỏi
- ✅ Kết quả bao gồm tên trạm, địa chỉ và trạng thái
- ✅ Các loại connector được liệt kê
- ✅ Trạng thái sẵn có theo thời gian thực được hiển thị

**Định dạng Phản hồi Mong đợi:**
```markdown
## ⚡ Trạm Sạc Gần Bạn

### VinFast Station - Hoàn Kiếm
📍 Địa chỉ: 123 Trần Hưng Đạo, Hoàn Kiếm, Hà Nội
🔌 Connectors: CCS2 (2 sẵn có), CHAdeMO (1 sẵn có)
⏰ Giờ mở cửa: 24/7
✅ Trạng thái: Có sẵn
```

### Kịch bản Kiểm thử 4: Cuộc hội thoại Nhiều lượt

Kiểm tra khả năng duy trì ngữ cảnh của agent qua nhiều lượt hội thoại.

**Cuộc hội thoại Kiểm thử:**

```
User: "Tôi muốn thuê xe VF8"
Agent: [Cung cấp thông tin VF8]

User: "Giá bao nhiêu?"
Agent: [Phải hiểu ngữ cảnh đang nói về giá VF8]

User: "Trạm sạc gần đó ở đâu?"
Agent: [Phải tìm trạm sạc gần vị trí VF8]
```

**Xác minh:**
- ✅ Agent duy trì ngữ cảnh cuộc hội thoại
- ✅ Đại từ và tham chiếu được hiểu đúng
- ✅ Session ID được giữ xuyên suốt các tin nhắn

### Kịch bản Kiểm thử 5: Xử lý Lỗi

Kiểm tra cách agent xử lý các câu hỏi không hợp lệ hoặc không rõ ràng.

**Các Trường hợp Kiểm thử:**

1. **Câu hỏi Mơ hồ:**
   ```
   User: "Xe"
   Kết quả mong đợi: Agent yêu cầu làm rõ
   ```

2. **Xe Không Có Sẵn:**
   ```
   User: "Tìm xe Tesla"
   Kết quả mong đợi: Agent giải thích Tesla không có, đề xuất thay thế
   ```

3. **Ngày Không hợp lệ:**
   ```
   User: "Thuê xe từ ngày 32/13"
   Kết quả mong đợi: Agent phát hiện ngày không hợp lệ và yêu cầu sửa
   ```

4. **Ngoài Phạm vi:**
   ```
   User: "Thời tiết hôm nay thế nào?"
   Kết quả mong đợi: Agent giải thích lịch sự chỉ có thể hỗ trợ về thuê xe EV
   ```

**Xác minh:**
- ✅ Agent xử lý lỗi một cách mượt mà
- ✅ Cung cấp thông báo lỗi hữu ích
- ✅ Đề xuất các phương án thay thế khi có thể

### Kiểm thử Hiệu năng

Kiểm tra hiệu năng hệ thống trong điều kiện sử dụng bình thường:

**Các Chỉ số Cần Theo dõi:**

1. **Thời gian Phản hồi:**
   - Truy vấn Knowledge Base: < 3 giây
   - Tìm kiếm xe: < 2 giây
   - Tìm trạm sạc: < 2 giây

2. **Tình trạng API:**
   ```bash
   curl http://localhost:8000/health
   ```
   Kết quả mong đợi: `200 OK` với trạng thái healthy

3. **Log Backend:**
   Kiểm tra lỗi trong console output của FastAPI

4. **Console Frontend:**
   Mở browser DevTools → Console
   - Không có lỗi JavaScript
   - Các API call thành công (tab Network)

### Danh sách Kiểm tra Tích hợp

Thực hiện danh sách kiểm tra toàn diện này:

- ✅ **Tích hợp Knowledge Base:**
  - Agent có thể truy xuất thông tin chính sách
  - Trích dẫn được bao gồm trong phản hồi
  - Các API call Bedrock thành công

- ✅ **Tích hợp Cơ sở dữ liệu:**
  - Tìm kiếm xe truy vấn PostgreSQL
  - Kết quả chính xác và cập nhật
  - Kết nối cơ sở dữ liệu ổn định

- ✅ **Backend API:**
  - Endpoint `/api/chat` hoạt động
  - Endpoint `/health` phản hồi
  - Quản lý session hoạt động đúng

- ✅ **Frontend UI:**
  - Tin nhắn hiển thị chính xác
  - Nhập liệu người dùng được thu thập
  - Trạng thái loading hoạt động
  - Markdown render đúng
  - Auto-scroll hoạt động

- ✅ **Xử lý Lỗi:**
  - Lỗi mạng được bắt
  - Đầu vào không hợp lệ được xử lý mượt mà
  - Người dùng nhận được phản hồi hữu ích

### Kiểm thử với Postman (Tùy chọn)

Kiểm thử backend API trực tiếp:

**1. Kiểm tra Health:**
```http
GET http://localhost:8000/health
```

**2. Yêu cầu Chat:**
```http
POST http://localhost:8000/api/chat
Content-Type: application/json

{
  "session_id": "test-session-123",
  "message": "Chính sách thuê xe là gì?"
}
```

**Phản hồi Mong đợi:**
```json
{
  "response": "## 📋 Chính sách thuê xe VinFast\n\n...",
  "data": null,
  "session_id": "test-session-123"
}
```

### Xử lý Sự cố Kiểm thử Thất bại

**Vấn đề: Knowledge Base trả về kết quả rỗng**
- Kiểm tra Knowledge Base đã được đồng bộ trong AWS Console
- Xác minh KNOWLEDGE_BASE_ID trong `.env`
- Test KB trực tiếp trong Bedrock console

**Vấn đề: Tìm kiếm xe không trả về kết quả**
- Kiểm tra cơ sở dữ liệu PostgreSQL có dữ liệu test
- Xác minh chuỗi kết nối DATABASE_URL
- Chạy truy vấn SQL trực tiếp: `SELECT * FROM vehicles;`

**Vấn đề: Không tìm thấy trạm sạc**
- Xác minh endpoint `/stations` của backend API hoạt động
- Kiểm tra dữ liệu trạm trong database
- Test API call: `curl http://localhost:8080/stations`

**Vấn đề: Frontend không kết nối được backend**
- Kiểm tra REACT_APP_API_URL trong frontend `.env`
- Xác minh backend CORS cho phép `http://localhost:3000`
- Kiểm tra console trình duyệt có lỗi network

### Mẫu Báo cáo Kiểm thử

Ghi lại kết quả kiểm thử của bạn:

```markdown
## Báo cáo Kiểm thử - EV Rental AI Agent

**Ngày:** 2024-12-20
**Người kiểm thử:** Tên của bạn

### Tóm tắt Kết quả
- Tổng số Test: 15
- Đạt: 14
- Thất bại: 1
- Tỷ lệ Thành công: 93%

### Kết quả Chi tiết

#### Tìm kiếm Knowledge Base
- [x] Truy vấn chính sách - ĐẠT
- [x] Giấy tờ yêu cầu - ĐẠT
- [x] Thông tin giá - ĐẠT
- [ ] Quy trình đặt xe - THẤT BẠI (phản hồi chậm)

#### Tìm kiếm Xe
- [x] Tìm theo địa điểm - ĐẠT
- [x] Tìm theo model - ĐẠT
- [x] Tìm theo khoảng ngày - ĐẠT

#### Tìm Trạm Sạc
- [x] Tìm theo quận - ĐẠT
- [x] Kiểm tra sẵn có - ĐẠT

### Vấn đề Phát hiện
1. Truy vấn quy trình đặt xe mất 7 giây (> ngưỡng 5s)
   - Nguyên nhân: Knowledge Base đồng bộ chưa hoàn tất
   - Sửa: Đồng bộ lại data source

### Khuyến nghị
- Theo dõi thời gian phản hồi trong lúc sử dụng cao điểm
- Thêm caching cho các câu hỏi thường gặp
- Triển khai rate limiting
```

---

**Thành công!** 🎉 EV Rental AI Agent của bạn đã được kiểm thử đầy đủ và hoạt động.

**Tiếp theo:** Chuyển sang [Cleanup](../5.7-Cleanup/) để xóa tài nguyên và tránh chi phí.
