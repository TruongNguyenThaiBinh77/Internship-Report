---
title: "Worklog Tuần 11"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Tuần 11: AWS Modernization & Module Booking/Blog Voltgo (17/11 - 21/11)

**Mục tiêu kép:** Hiện đại hóa ứng dụng trên AWS và xây dựng tính năng Booking/Blog cho Voltgo.

---

## PHẦN A: AWS - Hiện đại hóa Ứng dụng

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 17/11 | 2 | **Microservices Architecture** | - Thiết kế patterns microservices<br>- Triển khai API composition<br>- Cấu hình service mesh cơ bản |
| 18/11 | 3 | **CI/CD Pipeline** | - Setup CodePipeline cho tự động deploy<br>- Cấu hình CodeBuild cho testing<br>- Blue/Green deployment với CodeDeploy |
| 19/11 | 4 | **Container Orchestration Nâng cao** | - EKS nâng cao: HPA, VPA<br>- Triển khai service discovery<br>- Cấu hình ingress controllers |
| 20/11 | 5 | **Monitoring & Observability** | - CloudWatch Container Insights<br>- Tạo custom dashboards<br>- Setup alarms và notifications |
| 21/11 | 6 | **DevOps Best Practices** | - Review Infrastructure as Code<br>- Triển khai GitOps workflow<br>- Security scanning trong pipeline |

---

## PHẦN B: Voltgo - Module Booking & Blog

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 17/11 | 2 | **Booking Flow - Bước 1** | - Xây dựng booking wizard nhiều bước<br>- Bước 1: Chọn xe/trạm<br>- Bước 2: Chọn khung giờ |
| 18/11 | 3 | **Booking Flow - Bước 2** | - Bước 3: Xác nhận thông tin user<br>- Bước 4: Chọn phương thức thanh toán<br>- Tính giá với khuyến mãi |
| 19/11 | 4 | **Xác nhận Booking** | - Trang xác nhận booking<br>- Tạo QR code để nhận xe<br>- Gửi thông báo email/SMS |
| 20/11 | 5 | **Trang Danh sách Blog** | - Danh sách blog với categories<br>- Bài viết nổi bật/trending<br>- Tìm kiếm và lọc theo tag |
| 21/11 | 6 | **Trang Chi tiết Blog** | - Xem bài viết đầy đủ với rich content<br>- Sidebar bài viết liên quan<br>- Chia sẻ mạng xã hội, bình luận |

### Kết quả đạt được tuần 11:

* **AWS Modernization:**
  * Thiết kế patterns kiến trúc microservices
  * Xây dựng CI/CD pipeline hoàn chỉnh với CodePipeline
  * Cấu hình EKS nâng cao với auto-scaling
  * Monitoring toàn diện với Container Insights

* **Voltgo Booking & Blog:**
  * Hoàn thành booking flow với wizard 4 bước
  * Tạo QR code để nhận xe
  * Hệ thống blog với categories và tìm kiếm
  * Tích hợp chia sẻ mạng xã hội
