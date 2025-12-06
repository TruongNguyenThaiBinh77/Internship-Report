---
title: "Worklog Tuần 8"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Tuần 8: Tối ưu hóa Chi phí AWS & Khởi Động Dự Án Voltgo (27/10 - 31/10)

**Mục tiêu kép:** Tiếp tục học tập về tối ưu hóa chi phí và mạng nâng cao trên AWS, đồng thời bắt đầu triển khai dự án Voltgo Frontend.

---

## PHẦN A: AWS - Tối ưu hóa Chi phí và Mạng nâng cao

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 27/10 | 2 | **Cost Explorer & CUR** | - Phân tích chi phí theo Service, Region, Tag<br>- Kích hoạt Cost and Usage Report (CUR)<br>- Truy vấn CUR với Glue và Athena |
| 28/10 | 3 | **Right-Sizing** | - Sử dụng Compute Optimizer để nhận gợi ý<br>- Tích hợp CloudWatch Agent cho memory metrics |
| 29/10 | 4 | **Savings Plans & RIs** | - So sánh EC2 Instance vs Compute Savings Plans<br>- Lên kế hoạch cam kết 1 năm cho base load |
| 30/10 | 5 | **Transit Gateway** | - Triển khai hub-and-spoke network architecture<br>- Cấu hình routing tables giữa các VPCs |
| 31/10 | 6 | **VPC Flow Logs** | - Kích hoạt phân tích network traffic<br>- Debug REJECT status để xác định blocking rules |

---

## PHẦN B: Dự Án Voltgo - Vai trò Frontend Developer

Từ tuần 8, tôi bắt đầu tham gia **dự án Voltgo** - nền tảng thuê xe điện. Với vai trò **Frontend Developer**, tôi chịu trách nhiệm xây dựng các giao diện chính: **User, Login, Booking, Blog, Xe, Trạm**.

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 27/10 | 2 | **Project Kickoff** | - Hiểu yêu cầu business Voltgo<br>- Xác định 6 modules chính: User, Login, Booking, Blog, Xe, Trạm<br>- Tech stack: React.js + TypeScript |
| 28/10 | 3 | **Thiết lập Môi trường** | - Khởi tạo project với Vite + TypeScript<br>- Cấu trúc thư mục theo feature-based<br>- Git branching strategy (feature/user, feature/booking...) |
| 29/10 | 4 | **Design System** | - Định nghĩa Voltgo theme colors (xanh lá - thân thiện môi trường)<br>- Xây dựng shared components: VehicleCard, StationMarker, BookingCard |
| 30/10 | 5 | **Routing & State Management** | - Cấu hình React Router v6 cho tất cả pages<br>- Thiết lập Redux Toolkit slices cho từng module<br>- Tạo Axios API layer |
| 31/10 | 6 | **Layout Components** | - Xây dựng MainLayout với Header, Sidebar, Footer<br>- Triển khai responsive navigation menu<br>- Mobile hamburger menu |

### Kết quả đạt được tuần 8:

* **AWS Cost Optimization:**
  * Phân tích chi phí với Cost Explorer và CUR
  * Xác định tài nguyên over-provisioned với Compute Optimizer
  * Lên kế hoạch Savings Plans để giảm chi phí

* **Voltgo Frontend:**
  * Project khởi tạo với React + TypeScript
  * Design System định nghĩa với Voltgo branding
  * Core layout và routing structure hoàn thành
  * Sẵn sàng phát triển features từ Tuần 9
