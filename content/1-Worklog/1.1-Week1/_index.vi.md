---
title: "Worklog Tuần 1"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Tuần 1: Quản trị Định danh và Kiến trúc Mạng (08/09 – 12/09)

**Mục tiêu:** Thiết lập tài khoản AWS chuẩn doanh nghiệp và xây dựng mạng đám mây ảo (VPC) bảo mật.

### Các công việc đã hoàn thành trong tuần:

| Ngày  | Thứ | Nội dung                                 | Hoạt động chi tiết                                                                                                                                                              |
| ----- | --- | ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 08/09 | 2   | **Khởi tạo Tài khoản & Quản lý Chi phí** | - Tạo AWS Account, bảo mật Root User (kích hoạt MFA)<br>- Thiết lập AWS Budgets cảnh báo chi phí và sử dụng<br>- Nghiên cứu các gói AWS Support (Basic, Developer, Business)    |
| 09/09 | 3   | **IAM - Phần 1**                         | - Áp dụng nguyên tắc Đặc quyền Tối thiểu (Least Privilege)<br>- Tạo IAM Users và Groups (Admins, Developers, Auditors)<br>- Cấu hình Account Password Policy theo CIS Benchmark |
| 10/09 | 4   | **IAM - Phần 2**                         | - Tạo IAM Roles và Instance Profiles cho EC2<br>- Viết custom JSON policies cho quyền truy cập chi tiết<br>- Thực hành EC2 truy cập S3 qua Instance Metadata Service            |
| 11/09 | 5   | **Kiến trúc VPC - Lý thuyết & Thiết kế** | - Nghiên cứu khái niệm VPC vs Default VPC<br>- Quy hoạch không gian địa chỉ IP (CIDR 10.0.0.0/16)<br>- Thiết kế mô hình Multi-AZ với Public/Private Subnets                     |
| 12/09 | 6   | **Triển khai VPC**                       | - Tạo VPC, Subnets, Internet Gateway<br>- Cấu hình Route Tables cho Public/Private subnets<br>- Triển khai NAT Gateway cho Private subnet truy cập internet                     |

### Kết quả đạt được tuần 1:

- Hiểu các nhóm dịch vụ nền tảng của AWS:

  - Compute (Amazon EC2)
  - Networking (Amazon VPC)
  - Identity & Access Management (IAM)
  - Billing & Cost Management (AWS Budgets)

- Đã tạo và bảo mật thành công tài khoản AWS với MFA trên Root User

- Nắm vững các khái niệm IAM:

  - Tạo Users, Groups với Managed Policies
  - Viết custom JSON policies cho quyền truy cập chi tiết
  - IAM Roles cho EC2 (Instance Profiles)

- Thiết kế và triển khai VPC chuẩn doanh nghiệp:

  - Kiến trúc Multi-AZ đảm bảo High Availability
  - Public Subnets cho Load Balancers, Bastion Hosts
  - Private Subnets cho Databases, Application Servers
  - NAT Gateway cho truy cập internet an toàn từ Private subnet

- Áp dụng tư duy FinOps với AWS Budgets ngay từ ngày đầu
