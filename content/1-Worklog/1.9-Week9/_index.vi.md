---
title: "Worklog Tuần 9"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Tuần 9: Container AWS & Module Login/User Voltgo (03/11 - 07/11)

**Mục tiêu kép:** Làm chủ Docker và các nền tảng điều phối container trên AWS, đồng thời xây dựng các trang Authentication cho Voltgo.

---

## PHẦN A: AWS - Công nghệ Container

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 03/11 | 2 | **Docker Fundamentals** | - Viết Dockerfile tối ưu (Multi-stage build)<br>- Tạo ECR Repository<br>- Push private image lên ECR |
| 04/11 | 3 | **Amazon ECS & Fargate** | - Tạo Task Definition với CPU/RAM specs<br>- Deploy ECS Service với Fargate<br>- Tích hợp với Application Load Balancer |
| 05/11 | 4 | **Amazon EKS Setup** | - Tạo EKS cluster với eksctl<br>- Cấu hình Managed Node Groups<br>- AWS tự động patching và upgrades |
| 06/11 | 5 | **Deploy trên EKS** | - Viết K8s YAML manifests (Deployment, Service, Ingress)<br>- Cài đặt AWS Load Balancer Controller<br>- Auto-create ALB từ Ingress |
| 07/11 | 6 | **CI/CD cho Containers** | - Xây dựng CI/CD Pipeline cho ECS/EKS<br>- CodeCommit -> CodeBuild -> CodeDeploy<br>- Blue/Green Deployment strategy |

---

## PHẦN B: Voltgo - Module Login & User

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 03/11 | 2 | **Trang Đăng nhập** | - Xây dựng Login UI với React Hook Form + Yup validation<br>- Remember Me với localStorage<br>- Forgot Password flow với OTP |
| 04/11 | 3 | **Trang Đăng ký** | - Form đăng ký: họ tên, email, SĐT, mật khẩu<br>- Chọn loại user: Cá nhân/Doanh nghiệp<br>- Checkbox điều khoản sử dụng |
| 05/11 | 4 | **Authentication API** | - Kết nối POST /api/auth/login, /register<br>- JWT token management với auto-refresh<br>- Protected Routes cho Booking, Profile |
| 06/11 | 5 | **Trang User Profile** | - Hiển thị avatar, họ tên, email, SĐT, địa chỉ<br>- Form chỉnh sửa inline<br>- Upload GPLX (bắt buộc để thuê xe) |
| 07/11 | 6 | **Hoàn thiện Module User** | - Lịch sử booking trong trang User<br>- Tính năng xe yêu thích<br>- Quản lý phương thức thanh toán<br>- Cài đặt thông báo |

### Kết quả đạt được tuần 9:

* **AWS Containers:**
  * Triển khai containers trên ECS Fargate (serverless)
  * Thiết lập EKS cluster với managed node groups
  * Xây dựng CI/CD pipeline cho container applications

* **Voltgo Login & User:**
  * Hoàn thành trang Login/Register với validation
  * Tích hợp JWT authentication
  * User profile với avatar, upload GPLX
  * Lịch sử booking và phương thức thanh toán trong trang User
