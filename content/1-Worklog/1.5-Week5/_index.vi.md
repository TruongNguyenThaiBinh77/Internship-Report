---
title: "Worklog Tuần 5"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Tuần 5: Tư duy Vận hành và Hạ tầng dưới dạng Mã (06/10 - 10/10)

**Mục tiêu:** Loại bỏ thao tác thủ công, quản lý hạm đội máy chủ quy mô lớn và mã hóa hạ tầng.

### Các công việc đã hoàn thành trong tuần:

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 06/10 | 2 | **AWS Systems Manager** | - Cấu hình SSM Agent với IAM Role<br>- Run Command trên nhiều instances<br>- Thu thập software inventory cho auditing |
| 07/10 | 3 | **Session Manager Truy cập An toàn** | - Đóng port 22 (SSH) trên Security Groups<br>- Truy cập qua HTTPS Session Manager<br>- Log toàn bộ sessions vào S3/CloudWatch |
| 08/10 | 4 | **CloudFormation IaC** | - Viết YAML templates cho VPC và EC2<br>- Thực hành tạo, cập nhật, xóa Stack<br>- Sử dụng Change Sets và Drift Detection |
| 09/10 | 5 | **AWS CDK Cơ bản** | - Sử dụng TypeScript/Python cho hạ tầng<br>- Học các Construct levels (L1, L2, L3)<br>- Tạo VPC chỉ với một dòng code |
| 10/10 | 6 | **AWS CDK Nâng cao & Workshop** | - Xây dựng custom Constructs tái sử dụng<br>- Xử lý circular dependencies<br>- Quản lý biến môi trường với Context |

### Kết quả đạt được tuần 5:

* **Quản lý Hệ thống:**
  * Loại bỏ quản lý SSH key với Session Manager
  * Chạy commands trên fleet không cần truy cập từng máy
  * Thu thập inventory cho compliance auditing

* **Infrastructure as Code:**
  * Viết CloudFormation templates bằng YAML
  * Hiểu Stack lifecycle và state management
  * Phát hiện configuration drift

* **AWS CDK:**
  * Sử dụng ngôn ngữ lập trình cho hạ tầng
  * Xây dựng Constructs tái sử dụng cho tổ chức
  * Hoàn thành IaC Workshop challenges

* **Khái niệm quan trọng:**
  * IaC loại bỏ lỗi cấu hình thủ công
  * Session Manager là tiêu chuẩn vàng cho server access
  * CDK cung cấp abstraction cao hơn CloudFormation
