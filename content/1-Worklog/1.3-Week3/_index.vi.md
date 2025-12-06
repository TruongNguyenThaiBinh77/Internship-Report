---
title: "Worklog Tuần 3"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Tuần 3: Cơ sở dữ liệu và Dịch vụ quản lý (22/09 – 26/09)

**Mục tiêu:** Chuyển dịch từ việc tự quản lý cơ sở dữ liệu trên EC2 sang sử dụng các dịch vụ Managed Database (RDS, DynamoDB) để giảm tải vận hành.

### Các công việc đã hoàn thành trong tuần:

| Ngày  | Thứ | Nội dung                       | Hoạt động chi tiết                                                                                                                                            |
| ----- | --- | ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 22/09 | 2   | **Triển khai Amazon RDS**      | - Deploy RDS với MySQL/PostgreSQL engine<br>- Kích hoạt Multi-AZ cho high availability<br>- Phân tích Synchronous Replication và cơ chế automatic failover    |
| 23/09 | 3   | **Kết nối & Vận hành RDS**     | - Cấu hình Security Group chỉ cho phép App-Tier truy cập<br>- Tùy chỉnh cấu hình DB qua Parameter Groups<br>- Thực hành Automated Backups và Manual Snapshots |
| 24/09 | 4   | **Amazon DynamoDB - Phần 1**   | - Tạo bảng DynamoDB với Partition Key<br>- Hiểu sự khác biệt schema SQL vs NoSQL<br>- So sánh Provisioned vs On-Demand capacity modes                         |
| 25/09 | 5   | **DynamoDB Nâng cao - Phần 2** | - Thực hành các API: PutItem, GetItem, Query, Scan<br>- Hiểu hiệu quả Query vs Scan<br>- Tạo Global Secondary Index (GSI) cho truy vấn thay thế               |
| 26/09 | 6   | **Amazon ElastiCache**         | - Triển khai ElastiCache với Redis engine<br>- Áp dụng chiến lược caching Lazy Loading<br>- Đặt cache cluster trong Private Subnet để bảo mật                 |

### Kết quả đạt được tuần 3:

- **Cơ sở dữ liệu Quan hệ:**

  - Triển khai RDS với Multi-AZ đảm bảo high availability
  - Hiểu cơ chế synchronous replication và automatic failover
  - Cấu hình truy cập an toàn qua Security Groups

- **Cơ sở dữ liệu NoSQL:**

  - Thiết kế bảng DynamoDB với key schema phù hợp
  - Hiểu sự khác biệt Query (hiệu quả) vs Scan (tốn kém)
  - Triển khai GSI cho các mẫu truy vấn linh hoạt

- **Tầng Caching:**

  - Triển khai ElastiCache Redis cho application caching
  - Áp dụng Lazy Loading pattern giảm tải RDS
  - Đặt cache trong Private Subnet để tối ưu latency

- **Khái niệm quan trọng:**
  - Managed services giảm gánh nặng vận hành
  - Multi-AZ đảm bảo tính liên tục kinh doanh
  - Lựa chọn database phù hợp theo use case (SQL vs NoSQL)
