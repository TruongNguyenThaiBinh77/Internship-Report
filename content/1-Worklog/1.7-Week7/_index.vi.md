---
title: "Worklog Tuần 7"
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Tuần 7: Chiến lược Di chuyển và Khôi phục Thảm họa (20/10 - 24/10)

**Mục tiêu:** Chuyển đổi tải công việc từ On-Premise lên AWS và đảm bảo tính liên tục trong kinh doanh.

### Các công việc đã hoàn thành trong tuần:

| Ngày | Thứ | Nội dung | Hoạt động chi tiết |
| ---- | --- | -------- | ------------------ |
| 20/10 | 2 | **VM Import/Export** | - Giả lập On-Prem với VirtualBox<br>- Xuất VM ra định dạng .ova/.vmdk<br>- Upload lên S3 và import thành AMI |
| 21/10 | 3 | **Schema Conversion Tool (SCT)** | - Chuyển đổi Oracle schema sang Aurora PostgreSQL<br>- Tự động convert tables, keys, indexes<br>- Báo cáo Stored Procedures cần sửa thủ công |
| 22/10 | 4 | **Database Migration Service (DMS)** | - Tạo Replication Instance<br>- Cấu hình Source và Target endpoints<br>- Chạy Full Load + CDC cho minimal downtime |
| 23/10 | 5 | **Elastic Disaster Recovery (DRS)** | - Cài đặt Agent trên source servers<br>- Continuous block-level replication lên AWS<br>- Thực hiện DR Drill kiểm tra data integrity |
| 24/10 | 6 | **AWS Backup** | - Tạo Backup Plan tập trung cho EC2, EBS, RDS, DynamoDB<br>- Cấu hình Cross-Region Copy cho disaster protection |

### Kết quả đạt được tuần 7:

* **Server Migration:**
  * Di chuyển thành công VM từ VirtualBox lên EC2
  * Hiểu chiến lược Lift & Shift migration

* **Database Migration:**
  * Chuyển đổi heterogeneous database schema với SCT
  * Di chuyển dữ liệu với minimal downtime dùng DMS CDC

* **Disaster Recovery:**
  * Triển khai continuous replication với DRS
  * Test recovery với DR Drill
  * Đạt mục tiêu RPO/RTO thấp

* **Backup Strategy:**
  * Quản lý backup tập trung với AWS Backup
  * Cross-region copy cho regional disaster protection

* **Khái niệm quan trọng:**
  * 6 Rs of Migration (Rehost, Replatform, Refactor...)
  * RPO vs RTO trade-offs
  * Continuous replication vs periodic backup
