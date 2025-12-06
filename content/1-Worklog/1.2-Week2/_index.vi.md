---
title: "Worklog Tuần 2"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Tuần 2: Điện toán và Lưu trữ Cơ bản (15/09 – 19/09)

**Mục tiêu:** Triển khai máy chủ ảo (EC2), hiểu về các loại hình lưu trữ (EBS, S3) và các mô hình điện toán đơn giản hóa (Lightsail).

### Các công việc đã hoàn thành trong tuần:

| Ngày  | Thứ | Nội dung                            | Hoạt động chi tiết                                                                                                                                                                                      |
| ----- | --- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 15/09 | 2   | **Amazon EC2 - Khởi tạo & Kết nối** | - Phân tích các loại instance: T3 (Burstable), C5 (Compute), R5 (Memory)<br>- Khởi tạo Amazon Linux 2023 instance<br>- Kết nối SSH với Key Pairs (.pem/.ppk)                                            |
| 16/09 | 3   | **Lưu trữ EBS & Windows Workloads** | - Tạo và mount EBS volume gp3 vào Linux instance<br>- Triển khai Windows Server 2022, kết nối qua RDP<br>- Tạo EBS Snapshots để sao lưu                                                                 |
| 17/09 | 4   | **Môi trường Phát triển Cloud9**    | - Thiết lập IDE trên trình duyệt với AWS CLI, SAM, Docker cài sẵn<br>- Truy cập từ xa không cần mở port SSH<br>- Trải nghiệm code và terminal trực tiếp từ browser                                      |
| 18/09 | 5   | **Amazon S3 Cơ bản**                | - Tạo S3 Bucket và upload file media<br>- Cấu hình Static Website Hosting<br>- Viết Bucket Policy JSON cho public GetObject access                                                                      |
| 19/09 | 6   | **S3 Nâng cao & Bảo mật**           | - Phân tích Storage Classes: Standard, Intelligent-Tiering, Glacier<br>- Thiết lập Lifecycle Policy chuyển object cũ sang Glacier<br>- Bật Block Public Access, Versioning, Default Encryption (SSE-S3) |

### Kết quả đạt được tuần 2:

- **Thành thạo EC2:**

  - Hiểu các họ instance và trường hợp sử dụng
  - Khởi tạo và kết nối thành công cả Linux và Windows instances
  - Tạo EBS volumes và snapshots cho data persistence

- **Cloud Development:**

  - Thiết lập Cloud9 IDE loại bỏ vấn đề môi trường local
  - Trải nghiệm truy cập được quản lý không cần SSH public ports

- **Object Storage:**

  - Triển khai S3 static website với access policies phù hợp
  - Áp dụng tối ưu chi phí với Lifecycle Policies
  - Áp dụng best practices bảo mật: Block Public Access, Versioning, Encryption

- **Khái niệm quan trọng:**
  - EBS là lưu trữ bền vững độc lập với vòng đời EC2
  - S3 cung cấp object storage có khả năng mở rộng không giới hạn
  - Cơ chế incremental backup với Snapshots
