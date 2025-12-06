# Nội dung cập nhật cho các tuần còn lại

## Week 9 - Tasks Table

```markdown
### Các công việc cần triển khai trong tuần này:
| Task ID | Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Trạng thái | Nguồn tài liệu |
| --- | --- | --- | --- | --- | --- | --- |
| T9.1 | 2 | **VPC - Enable Flow Logs:** <br> - Bật Flow Logs cho VPC <br> - Đích đến: CloudWatch Logs Group `/aws/vpc/flowlogs` | 03/11/2025 | 03/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T9.2 | 2 | **Testing - Generate Deny:** <br> - Thử SSH từ IP không có trong Security Group <br> - Tạo ra các bản ghi REJECT | 03/11/2025 | 04/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T9.3 | 3 | **Logs - Insights Query:** <br> - Viết query đếm số gói tin bị từ chối theo Source IP <br> - `filter action="REJECT" | stats count() by srcAddr` | 05/11/2025 | 05/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T9.4 | 4 | **Cost - Compute Optimizer:** <br> - Truy cập Compute Optimizer <br> - Xem khuyến nghị (cần ít nhất 12-24h dữ liệu) | 06/11/2025 | 07/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T9.5 | 5 | **Cost - Cost Explorer:** <br> - Phân tích chi phí theo ngày và dịch vụ <br> - Group by Service <br> - Xác định EC2 hay RDS tốn nhiều tiền nhất | 08/11/2025 | 09/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 9:

* **Điều tra số:**
  * Đã xác định địa chỉ IP nào đang cố quét port SSH
  * Phát hiện các pattern tấn công
  * Có thể trace được network path

* **Tiết kiệm:**
  * Compute Optimizer chỉ ra instances đang chạy dưới 5% CPU
  * Xác nhận t3.micro phù hợp hoặc có thể gom lại
  * Phát hiện tài nguyên không sử dụng

* **Kỹ năng:**
  * Thành thạo cú pháp query của Logs Insights
  * Kỹ năng quan trọng để xử lý sự cố nhanh
  * Hiểu về VPC Flow Logs format

* **FinOps:**
  * Biết cách phân tích chi phí theo nhiều chiều
  * Hiểu về Cost Allocation Tags
  * Có thể dự báo chi phí hàng tháng
```

## Week 10 - Tasks Table

```markdown
### Các công việc cần triển khai trong tuần này:
| Task ID | Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Trạng thái | Nguồn tài liệu |
| --- | --- | --- | --- | --- | --- | --- |
| T10.1 | 2 | **DynamoDB - Create Table:** <br> - Tạo bảng `Books` với Partition Key là ISBN (String) <br> - Cấu hình chế độ On-Demand Capacity | 10/11/2025 | 10/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T10.2 | 2 | **IAM - Lambda Role:** <br> - Tạo Role cho Lambda <br> - Quyền: PutItem, GetItem, Scan trên bảng Books <br> - Quyền ghi log CloudWatch | 10/11/2025 | 11/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T10.3 | 3 | **Lambda - Function Logic:** <br> - Viết hàm `add_book` (Python) nhận JSON và ghi DynamoDB <br> - Viết hàm `get_books` để đọc dữ liệu | 12/11/2025 | 12/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T10.4 | 4 | **API Gateway - REST API:** <br> - Tạo API `BookStoreAPI` <br> - Tạo resource `/books` và method POST, GET <br> - Tích hợp với Lambda functions | 13/11/2025 | 13/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T10.5 | 5 | **API Gateway - Deploy:** <br> - Deploy API ra Stage `dev` <br> - Lấy Invoke URL | 14/11/2025 | 14/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T10.6 | 6 | **Testing - Postman:** <br> - Gửi POST request thêm sách <br> - Gửi GET request kiểm tra danh sách trả về | 15/11/2025 | 16/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 10:

* **Sản phẩm:**
  * Một backend API hoàn chỉnh hoạt động
  * Không cần bất kỳ máy chủ nào (No EC2)
  * Truly serverless architecture

* **Hiệu năng:**
  * Tốc độ phản hồi cực nhanh (< 100ms)
  * Khả năng chịu tải hàng nghìn request/giây mặc định
  * Auto scaling không cần cấu hình

* **Chi phí:**
  * Gần như $0 trong giai đoạn phát triển
  * Nhờ Free Tier của Lambda và DynamoDB
  * Pay-per-request model

* **Kiến trúc:**
  * Hiểu về Microservices architecture
  * Event-driven programming
  * API-first design
  * NoSQL data modeling
```

## Week 11 - Complete Content

```markdown
---
title: "Worklog Tuần 11"
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 11:

* Kiểm toán Kiến trúc: Đánh giá lại toàn bộ hạ tầng dựa trên AWS Well-Architected Tool.
* Quản lý Hạn mức: Kiểm tra Service Quotas và hiểu quy trình yêu cầu tăng hạn mức.
* Vệ sinh Tài nguyên: Tìm và xóa tài nguyên "mồ côi" (Orphaned resources).
* Ngân sách Nâng cao: Thiết lập AWS Budgets với cảnh báo dự báo (Forecasted breach).

### Các công việc cần triển khai trong tuần này:
| Task ID | Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Trạng thái | Nguồn tài liệu |
| --- | --- | --- | --- | --- | --- | --- |
| T11.1 | 2 | **Governance - Quota Check:** <br> - Kiểm tra hạn mức vCPU cho dòng instance <br> - Running On-Demand Standard instances | 17/11/2025 | 17/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T11.2 | 2 | **Cost - Budget Forecast:** <br> - Tạo Budget cảnh báo nếu dự báo cuối tháng vượt $10 <br> - Thay vì đợi vượt rồi mới báo | 17/11/2025 | 18/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T11.3 | 3 | **WAF - Tool Review:** <br> - Mở AWS Well-Architected Tool <br> - Tạo Workload mới <br> - Trả lời câu hỏi trong trụ cột Security | 19/11/2025 | 19/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T11.4 | 4 | **Cleanup - EBS Audit:** <br> - Tìm EBS Volume có trạng thái Available <br> - Xóa để cắt giảm chi phí | 20/11/2025 | 20/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T11.5 | 5 | **Cleanup - EIP Audit:** <br> - Release Elastic IP không gắn vào instance nào <br> - AWS tính phí phạt cho EIP không sử dụng | 21/11/2025 | 23/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 11:

* **Báo cáo rủi ro:**
  * Well-Architected Tool chỉ ra High Risk Issue
  * Database Tuần 4 đang chạy Single-AZ
  * Nếu AZ sập, DB mất kết nối
  * Cần cân nhắc Multi-AZ cho production

* **Tối ưu:**
  * Đã xóa 2 volume EBS 10GB còn sót lại
  * Tiết kiệm khoảng $2/tháng
  * Release 1 Elastic IP không dùng
  * Tránh phí phạt $3.6/tháng

* **Nhận thức:**
  * "Kiến trúc tốt" là quá trình liên tục
  * Không phải đích đến
  * Cần review và cải thiện thường xuyên
  * Well-Architected Framework là kim chỉ nam

* **Governance:**
  * Hiểu về Service Quotas và Limits
  * Biết cách request tăng quota
  * Có thể dự báo khi cần scale
  * Proactive capacity planning
```

## Week 12 - Complete Content

```markdown
---
title: "Worklog Tuần 12"
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

* Tổng hợp Kiến thức: Triển khai dự án cuối khóa (Capstone) kết hợp IaaS và PaaS.
* Chứng nhận: Hoàn thành bài thi thử (Mock Exam) cho chứng chỉ SAA-C03 với điểm số >70%.
* Hồ sơ Năng lực: Cập nhật CV, GitHub Profile với các dự án đã làm.
* Dọn dẹp: Hủy bỏ toàn bộ tài nguyên để tránh phát sinh chi phí sau khóa học.

### Các công việc cần triển khai trong tuần này:
| Task ID | Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Trạng thái | Nguồn tài liệu |
| --- | --- | --- | --- | --- | --- | --- |
| T12.1 | 2 | **Capstone - Architecture:** <br> - Vẽ sơ đồ kiến trúc cho dự án cuối khóa (AWS Icons) <br> - Bao gồm: ALB, ASG, RDS, S3, CloudFront | 24/11/2025 | 24/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T12.2 | 3 | **Capstone - Deployment:** <br> - Triển khai dự án sử dụng CDK hoặc CloudFormation <br> - Đảm bảo ứng dụng chạy tốt, kết nối DB thành công | 25/11/2025 | 26/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T12.3 | 4 | **Career - Community:** <br> - Tham gia nhóm "AWS Study Group" trên Facebook/LinkedIn <br> - Kết nối với các mentor FCJ Workforce | 27/11/2025 | 27/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T12.4 | 5 | **Exam - Practice Test:** <br> - Làm bài test 65 câu trong 130 phút (mô phỏng thi thật) <br> - Review các câu sai | 28/11/2025 | 28/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |
| T12.5 | 6 | **Cleanup - NUKE:** <br> - Sử dụng công cụ aws-nuke (hoặc xóa thủ công) <br> - Dọn sạch tài khoản <br> - Kiểm tra lại ở mọi Region | 29/11/2025 | 30/11/2025 | Hoàn thành | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 12:

* **Sản phẩm:**
  * Một GitHub Repository chứa code CDK
  * Kiến trúc 3-Tier chuẩn mực
  * Documentation đầy đủ
  * README với architecture diagram

* **Tự tin:**
  * Sẵn sàng cho kỳ thi chứng chỉ AWS SAA-C03
  * Sẵn sàng cho phỏng vấn thực tập sinh Cloud
  * Có portfolio để showcase
  * Hiểu rõ các dịch vụ AWS core

* **Hoàn tất:**
  * Tài khoản AWS sạch sẽ
  * Không còn chi phí phát sinh
  * Đã backup tất cả artifacts quan trọng
  * Sẵn sàng cho hành trình tiếp theo

* **Hành trình:**
  * Từ "không biết gì" về Cloud
  * Đến "AWS Builder" thực thụ
  * 12 tuần = 84 ngày thay đổi
  * Foundation vững chắc cho career Cloud Engineer
```

---

## Hướng dẫn cập nhật:

1. Copy nội dung Week 9 vào file `1.9-Week9\_index.vi.md` (thay thế phần Tasks và Results)
2. Copy nội dung Week 10 vào file `1.10-Week10\_index.vi.md` (thay thế phần Tasks và Results)
3. Copy TOÀN BỘ nội dung Week 11 vào file `1.11-Week11\_index.vi.md`
4. Copy TOÀN BỘ nội dung Week 12 vào file `1.12-Week12\_index.vi.md`
