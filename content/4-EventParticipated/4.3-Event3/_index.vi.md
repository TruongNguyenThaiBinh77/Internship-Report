---
title: "Event 3"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Bài thu hoạch "AWS Cloud Mastery Series #2: From DevOps, IaC to Containers & Observability"

### I. TỔNG QUAN SỰ KIỆN

**Tên sự kiện:** AWS Cloud Mastery Series #2: From DevOps, IaC to Containers & Observability

**Mục tiêu tham dự:**

1. **Chuẩn hóa tư duy (Mindset):** Hiểu sâu về Chu trình giá trị (Value Cycle) và vai trò cốt lõi của DevOps
2. **Hiện đại hóa hạ tầng (IaC):** Chuyển dịch từ thao tác thủ công (ClickOps) sang quản lý hạ tầng bằng mã (Infrastructure as Code)
3. **Tối ưu hóa ứng dụng (Containerization):** Nắm vững chiến lược lựa chọn nền tảng container phù hợp (App Runner, ECS, EKS)
4. **Giám sát toàn diện (Observability):** Xây dựng hệ thống giám sát chủ động với CloudWatch và X-Ray

**Danh Sách Diễn Giả:**

Đội ngũ chuyên gia AWS & Cloud Engineers: Chia sẻ về kiến trúc hệ thống, chiến lược Platform Engineering và demo kỹ thuật chuyên sâu.

### II. NỘI DUNG KIẾN THỨC TRỌNG TÂM

Dưới sự chia sẻ của các chuyên gia AWS và kỹ sư Cloud, tôi đã đúc kết được các khối kiến thức nền tảng sau:

#### 1. Tư duy DevOps & CI/CD Pipeline

Sự kiện bắt đầu bằng việc định nghĩa lại DevOps không chỉ là công cụ, mà là văn hóa tối ưu hóa dòng chảy giá trị.

**Chu trình giá trị (Value Cycle):** Quy trình khép kín 5 bước nhằm tăng tốc độ giao hàng (Speed) nhưng vẫn đảm bảo sự ổn định (Stability).

**Chiến lược Pipeline hiệu quả:**

Phân biệt rõ Concepts:
- **Continuous Integration (CI):** Fail fast, tích hợp code hàng ngày
- **Continuous Delivery:** Tự động đến Staging, cần con người duyệt để lên Production
- **Continuous Deployment:** Tự động hóa 100% đến Production

**Nguyên tắc "Build Once, Deploy Anywhere":** Source code chỉ được build một lần duy nhất thành gói Binary (Artifact). Các môi trường sau (Staging, Prod) sử dụng lại chính Artifact này để đảm bảo tính nhất quán tuyệt đối.

**Điều kiện Fail Fast:** Pipeline phải dừng ngay lập tức khi gặp lỗi biên dịch, vi phạm Code Style, lỗ hổng bảo mật hoặc test quá chậm.

#### 2. Infrastructure as Code (IaC) - Từ ClickOps đến Code

Phần này giải quyết bài toán loại bỏ thói quen thao tác tay ("ClickOps") dễ gây lỗi và khó mở rộng. Tôi đã phân tích sâu 3 công cụ chủ đạo:

**AWS CloudFormation (Native):**
- Sử dụng YAML/JSON
- Quản lý tài nguyên theo đơn vị Stack
- Xóa Stack đồng nghĩa xóa toàn bộ tài nguyên liên quan

**Terraform (Multi-Cloud):**
- Sử dụng ngôn ngữ HCL
- Điểm mạnh là hỗ trợ đa nền tảng
- Quy trình làm việc an toàn: $Code \rightarrow Plan \text{ (Review thay đổi)} \rightarrow Apply$

**AWS CDK (Cloud Development Kit):**
- Cho phép định nghĩa hạ tầng bằng ngôn ngữ lập trình (Python, TypeScript...)
- **Constructs:** Từ L1 (Cấu hình chi tiết) đến L3 (Patterns kiến trúc phức tạp)
- **Drift Detection:** Tính năng quan trọng giúp phát hiện sự sai lệch giữa Code và Thực tế (do ai đó sửa tay trên Console)

#### 3. Chiến lược Containerization

Việc lựa chọn nền tảng chạy Container phụ thuộc vào quy mô và nhu cầu:

- **Amazon ECS:** Đơn giản, tích hợp sâu với AWS, phù hợp cho team muốn vận hành nhanh gọn
- **Amazon EKS:** Dựa trên Kubernetes chuẩn, hệ sinh thái lớn, phù hợp cho Enterprise hoặc hệ thống phức tạp/Hybrid
- **AWS App Runner:** Giải pháp "Zero-ops" cho Web App/API, tự động từ Source/Image ra URL HTTPS mà không cần cấu hình server

**Mô hình tính toán (Compute Options):**
- **EC2 Launch Type:** Kiểm soát cao nhất nhưng tốn công vận hành (patching, scaling)
- **AWS Fargate (Serverless):** AWS lo hạ tầng, người dùng chỉ cần định nghĩa CPU/RAM cho Task

#### 4. Observability - Giám sát & Tối ưu

Khép kín vòng đời phát triển bằng khả năng quan sát sâu:

- **Amazon CloudWatch:** "Mắt và Tai" của hệ thống (Metrics, Logs, Alarms)
- **AWS X-Ray:** Giải quyết bài toán "mò kim đáy bể" trong Microservices bằng Distributed Tracing (theo vết request đi qua nhiều service để tìm điểm nghẽn)

### III. ĐÁNH GIÁ & BÀI HỌC KINH NGHIỆM

Tham gia chuỗi workshop này đã thay đổi đáng kể nhận thức và kỹ năng của tôi:

#### 1. Sự chuyển dịch từ "Ops" sang "Platform Engineering"

Tôi nhận ra vai trò của DevOps hiện đại không phải là chạy theo Developer để deploy code thủ công. DevOps là người kiến tạo nên "Đường cao tốc" (Pipeline & Platform). Một Platform tốt cho phép Developer có khả năng Self-service (tự phục vụ) việc tạo môi trường và deploy code nhanh chóng nhưng vẫn nằm trong hành lang an toàn (Governance) mà team DevOps thiết lập.

#### 2. Kỷ luật trong vận hành (Operational Discipline)

Bài học về Artifact Management và Drift Detection là những quy tắc vàng. Trong môi trường Enterprise, sự nhất quán là sống còn. Việc build khác nhau ở các môi trường hay sửa tay (manual changes) vào hệ thống đang quản lý bằng code cần phải bị nghiêm cấm.

#### 3. Chiến lược chọn công cụ thông minh

Không có công cụ "tốt nhất", chỉ có công cụ "phù hợp nhất":

- Cần sự ổn định tuyệt đối và hỗ trợ sâu nhất dịch vụ mới của AWS $\rightarrow$ Chọn CloudFormation
- Doanh nghiệp dùng Multi-cloud hoặc Hybrid-cloud $\rightarrow$ Terraform là tối ưu
- Team Developer mạnh về lập trình, cần dựng kiến trúc phức tạp nhanh và tái sử dụng code $\rightarrow$ AWS CDK
- Web App đơn giản $\rightarrow$ Dùng App Runner thay vì tốn nguồn lực vận hành cụm Kubernetes

### IV. KẾT LUẬN

Series "DevOps & IaC Mastery" đã cung cấp một lộ trình hoàn chỉnh cho hành trình Cloud:

- **Tư duy:** Chuyển từ làm thủ công sang tự động hóa và đo lường bằng số liệu
- **Hạ tầng:** Làm chủ IaC để có hệ thống mở rộng, tái tạo được và kiểm soát sai lệch (Drift)
- **Vận hành:** Kết hợp Containerization linh hoạt và Observability sâu sát để đảm bảo hệ thống ổn định, hiệu năng cao

Đây là nền tảng kiến thức vững chắc để tôi tự tin xây dựng và vận hành các hệ thống phần mềm quy mô lớn trên AWS.

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của bạn tại đây

> Tổng thể, workshop đã giúp tôi có cái nhìn toàn diện về DevOps hiện đại, từ mindset, công cụ IaC, chiến lược containerization đến observability, tạo nền tảng vững chắc cho việc xây dựng và vận hành hệ thống Cloud-native.
