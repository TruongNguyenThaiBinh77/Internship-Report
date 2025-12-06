---
title: "Worklog Tuần 4"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Tuần 4: Khả năng mở rộng, Giám sát và Mạng phân phối (29/09 – 03/10)

**Mục tiêu:** Tự động hóa khả năng mở rộng hệ thống, thiết lập giám sát toàn diện và tối ưu hóa phân phối nội dung toàn cầu.

### Các công việc đã hoàn thành trong tuần:

| Ngày  | Thứ | Nội dung                       | Hoạt động chi tiết                                                                                                                                                               |
| ----- | --- | ------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 29/09 | 2   | **EC2 Auto Scaling**           | - Tạo Launch Templates với AMI, Instance Type, Security Group<br>- Thiết lập Auto Scaling Group (Min=2, Max=4, Desired=2)<br>- Cấu hình Target Tracking Scaling Policy (CPU 50%) |
| 30/09 | 3   | **Giám sát Amazon CloudWatch** | - Theo dõi các metrics chuẩn (CPU, Disk I/O, Network)<br>- Cài đặt CloudWatch Agent cho Memory metrics<br>- Tạo Alarms với SNS notifications                                     |
| 01/10 | 4   | **Giám sát Nâng cao & Logs**   | - Cấu hình CloudWatch Agent đẩy application logs<br>- Tạo CloudWatch Dashboard tổng quan sức khỏe hệ thống<br>- Tìm hiểu tích hợp Grafana                                        |
| 02/10 | 5   | **Amazon Route 53 DNS**        | - Tạo Hosted Zone quản lý tên miền<br>- Thực hành các routing policies: Simple, Failover, Latency-based<br>- Cấu hình Health Checks cho automatic failover                       |
| 03/10 | 6   | **Amazon CloudFront CDN**      | - Triển khai CloudFront distribution cho S3 static content<br>- Cấu hình OAC (Origin Access Control)<br>- Tùy chỉnh TTL caching policies                                         |

### Kết quả đạt được tuần 4:

- **Auto Scaling:**

  - Triển khai Auto Scaling Group với Launch Templates
  - Test scale out/in với công cụ stress
  - Tích hợp với Application Load Balancer

- **Monitoring:**

  - Xây dựng CloudWatch Dashboard toàn diện
  - Cấu hình alarms cho CPU, Memory, Disk metrics
  - Thiết lập SNS notifications cho alerts

- **DNS & CDN:**

  - Cấu hình Route 53 với nhiều routing policies
  - Triển khai CloudFront cho phân phối nội dung toàn cầu
  - Áp dụng OAC cho truy cập S3 an toàn qua CDN

- **Khái niệm quan trọng:**
  - Horizontal scaling với Auto Scaling Groups
  - Giám sát chủ động vs xử lý sự cố bị động
  - Edge locations cho phân phối nội dung độ trễ thấp
