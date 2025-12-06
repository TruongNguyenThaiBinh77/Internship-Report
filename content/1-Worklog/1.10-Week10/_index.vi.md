---
title: "Worklog Tuần 10"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Tuần 10: Serverless AWS & Module Xe/Trạm Voltgo (10/11 - 14/11)

**Mục tiêu kép:** Xây dựng ứng dụng serverless trên AWS và phát triển tính năng Xe/Trạm cho Voltgo.

---

## PHẦN A: AWS - Kiến trúc Serverless

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 10/11 | 2 | **Bộ ba Serverless** | - Viết AWS Lambda cho CRUD operations<br>- Tích hợp với DynamoDB<br>- Xây dựng REST API với API Gateway |
| 11/11 | 3 | **Serverless Auth & Security** | - Deploy Cognito Authorizer trên API Gateway<br>- Cấu hình Custom Domains và SSL |
| 12/11 | 4 | **Event-Driven Architecture** | - Xử lý orders với SQS và SNS<br>- Cấu hình S3 triggers tạo thumbnail |
| 13/11 | 5 | **Step Functions** | - Xây dựng workflow orchestration<br>- Tạo quy trình phê duyệt: Kiểm tra kho -> Trừ tiền -> Gửi email |
| 14/11 | 6 | **X-Ray Tracing** | - Kích hoạt distributed tracing<br>- Quan sát service map: API Gateway -> Lambda -> DynamoDB |

---

## PHẦN B: Voltgo - Module Xe & Trạm

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 10/11 | 2 | **Trang Danh sách Xe** | - Xây dựng danh sách xe với grid/list toggle<br>- VehicleCard: hình ảnh, tên, loại, giá, pin, trạng thái<br>- Filter theo loại, giá, phạm vi |
| 11/11 | 3 | **Trang Chi tiết Xe** | - Image gallery, hiển thị thông số<br>- Bảng giá (giờ, ngày, tuần)<br>- Calendar lịch available, phần đánh giá |
| 12/11 | 4 | **Trang Danh sách Trạm** | - Danh sách trạm với StationCard<br>- Tích hợp Google Maps/Mapbox<br>- Trạm gần nhất với Geolocation API |
| 13/11 | 5 | **Trang Chi tiết Trạm** | - Thông tin đầy đủ: địa chỉ, giờ mở cửa, tiện ích<br>- Xe available tại trạm<br>- Trạng thái slot sạc, chỉ đường |
| 14/11 | 6 | **Map View & Real-time** | - Bản đồ full-screen với tất cả trạm/xe<br>- Custom markers (trạm=xanh, xe=vàng)<br>- Marker clustering, cập nhật real-time |

### Kết quả đạt được tuần 10:

* **AWS Serverless:**
  * Xây dựng serverless API hoàn chỉnh với Lambda, API Gateway, DynamoDB
  * Triển khai event-driven architecture với SQS/SNS
  * Điều phối workflows với Step Functions
  * Kích hoạt distributed tracing với X-Ray

* **Voltgo Xe & Trạm:**
  * Hoàn thành trang Danh sách và Chi tiết Xe
  * Trang Trạm với tích hợp bản đồ
  * Cập nhật real-time trạng thái xe/trạm
  * Geolocation cho trạm gần nhất
