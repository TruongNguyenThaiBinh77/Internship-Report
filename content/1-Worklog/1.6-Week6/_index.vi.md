---
title: "Worklog Tuần 6"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Tuần 6: Kiến trúc Bảo mật Đa lớp (13/10 - 17/10)

**Mục tiêu:** Xây dựng pháo đài số bảo vệ dữ liệu và ứng dụng trước các mối đe dọa mạng hiện đại.

### Các công việc đã hoàn thành trong tuần:

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 13/10 | 2 | **AWS WAF** | - Triển khai WAF trên ALB/CloudFront<br>- Cấu hình rules chống SQL Injection, XSS<br>- Tạo Rate-based rules chống DDoS |
| 14/10 | 3 | **AWS KMS Mã hóa** | - Tạo Customer Managed Keys (CMK)<br>- Cấu hình Key Policy phân tách admin/user<br>- Kích hoạt mã hóa trên EBS và S3 |
| 15/10 | 4 | **Secrets Manager** | - Lưu trữ mật khẩu RDS trong Secrets Manager<br>- Cấu hình automatic rotation với Lambda<br>- Cập nhật ứng dụng lấy secrets qua API |
| 16/10 | 5 | **GuardDuty Phát hiện Mối đe dọa** | - Kích hoạt intelligent threat detection<br>- Phân tích CloudTrail, VPC Flow Logs, DNS Logs<br>- Cấu hình EventBridge alerts cho high-severity findings |
| 17/10 | 6 | **Amazon Cognito** | - Tạo User Pool cho app authentication<br>- Cấu hình Identity Pool cho temporary AWS credentials<br>- Cho phép end users upload trực tiếp lên S3 |

### Kết quả đạt được tuần 6:

* **Bảo mật Ứng dụng:**
  * Triển khai WAF bảo vệ chống OWASP Top 10
  * Áp dụng rate limiting chống DDoS

* **Mã hóa Dữ liệu:**
  * Tạo và quản lý CMK với key policies phù hợp
  * Mã hóa data at rest trên EBS, S3, RDS

* **Quản lý Secrets:**
  * Loại bỏ hardcoded credentials trong ứng dụng
  * Tự động hóa password rotation

* **Phát hiện Mối đe dọa:**
  * Kích hoạt ML-based threat detection với GuardDuty
  * Thiết lập automated alerting cho security incidents

* **Identity Federation:**
  * Xây dựng user authentication với Cognito User Pools
  * Kích hoạt federated access với Identity Pools
