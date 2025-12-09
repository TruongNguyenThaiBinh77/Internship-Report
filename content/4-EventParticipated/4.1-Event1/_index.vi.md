---
title: "Event 1"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài thu hoạch "Vietnam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders"

**Chủ đề (Track 1):** GenAI & Data (Trí tuệ nhân tạo tạo sinh & Dữ liệu)

### I. MỤC TIÊU THAM DỰ

Việc tham dự sự kiện nhằm cập nhật các xu hướng và giải pháp mới nhất trên AWS, cụ thể tập trung vào 4 mục tiêu chính:

1. **Chiến lược GenAI toàn diện:** Nắm bắt cách xây dựng quy trình phát triển phần mềm định hướng AI (AI-DLC) và các chiến lược GenAI mới nhất
2. **Bảo mật doanh nghiệp:** Hiểu sâu về bảo mật trong GenAI và AI Agents để đảm bảo an toàn dữ liệu
3. **Nền tảng dữ liệu:** Học cách xây dựng nền tảng dữ liệu thống nhất (Unified Data Foundation) tối ưu cho Analytics và AI
4. **Kết nối chuyên gia:** Trao đổi trực tiếp với đội ngũ kỹ sư và chuyên gia từ AWS

**Diễn giả tham gia:**

Đội ngũ AWS: Jun Kai Loke (AI/ML Specialist), Kien Nguyen, Tamelly Lim, Binh Tran, Taiki Dang (Solutions Architects), Michael Armentano (Principal WW GTM Specialist).

### II. NỘI DUNG CHUYÊN MÔN TRỌNG TÂM

#### 1. Nền tảng dữ liệu thống nhất (Unified Data Platform)

Để AI hoạt động hiệu quả, dữ liệu cần được xử lý liền mạch. AWS nhấn mạnh mô hình Zero-ETL và phá vỡ các "ốc đảo dữ liệu" (silos):

- **Quy trình End-to-End:** Từ thu thập (Ingestion) $\rightarrow$ Lưu trữ (Storage) $\rightarrow$ Xử lý (Processing) $\rightarrow$ Truy cập (Access) $\rightarrow$ Quản trị (Governance)
- **Hệ sinh thái dịch vụ:** Kết hợp chặt chẽ giữa Amazon S3, Glue, Redshift, Lake Formation và OpenSearch
- **Tư duy Self-service:** Trao quyền cho các nhóm dự án tự khai thác dữ liệu nhưng vẫn đảm bảo tuân thủ quy chuẩn chung

#### 2. Chiến lược GenAI & Amazon Bedrock

- **Amazon Bedrock:** Đóng vai trò trung tâm trong việc lựa chọn mô hình (Foundation Models), triển khai RAG (Retrieval-Augmented Generation), và tối ưu hóa chi phí/độ trễ
- **AgentCore & Amazon Nova:** Hỗ trợ mạnh mẽ các framework Agent hiện đại như CrewAI, LangGraph, LlamaIndex, giúp xây dựng các tác vụ tự động hóa phức tạp

#### 3. Bảo mật đa lớp cho GenAI (Securing GenAI)

Bảo mật không chỉ nằm ở hạ tầng mà phải áp dụng theo mô hình "Defense in Depth" (Phòng thủ chiều sâu):

- **3 lớp bảo mật:** Hạ tầng (Infrastructure) $\rightarrow$ Mô hình (Model) $\rightarrow$ Ứng dụng (Application)
- **5 trụ cột chính:** Tuân thủ (Compliance), Quyền riêng tư (Privacy), Kiểm soát (Controls), Quản lý rủi ro (Risk Management), và Khả năng phục hồi (Resilience)
- **Công cụ thực tế:** Sử dụng Bedrock Guardrails để kiểm duyệt nội dung đầu ra/đầu vào và OpenTelemetry để giám sát (Observability)

#### 4. AI-Driven Development Lifecycle (AI-DLC)

Đây là sự chuyển dịch quan trọng trong tư duy phát triển phần mềm:

- **Tiến hóa:** Chuyển từ AI-Assisted (AI hỗ trợ code) $\rightarrow$ AI-Driven (AI dẫn dắt) $\rightarrow$ AI-Managed (AI quản lý vận hành)
- **Thực thi:** Tích hợp AI vào mọi khâu: từ IaC (Infrastructure as Code), kiểm thử tự động (Automated Testing) đến quản lý rủi ro

#### 5. Amazon SageMaker – Unified Studio

- Môi trường hợp nhất cho Data, Analytics và AI, hỗ trợ kiến trúc Lakehouse
- Tích hợp MLOps toàn diện (Pipelines, Registry, Monitoring) giúp tăng tốc đưa ứng dụng GenAI ra thị trường

### III. BÀI HỌC & TƯ DUY ĐÚC KẾT

Từ các nội dung trên, tôi rút ra được 3 bài học cốt lõi cho việc phát triển dự án:

#### Tư duy Thiết kế (Design Mindset):

- Cần xây dựng hệ thống Data & AI theo tư duy "End-to-End" ngay từ đầu, tránh rời rạc
- Nguyên tắc quản trị (Governance) phải đi đôi với khả năng tự phục vụ (Self-service)

#### Kiến trúc Kỹ thuật (Technical Architecture):

- Tận dụng tối đa Zero-ETL (tích hợp S3 $\leftrightarrow$ Redshift/Aurora/DynamoDB) để giảm thiểu công sức vận hành đường ống dữ liệu
- Sử dụng AI Agents để tự động hóa quy trình thay vì chỉ dùng AI như một công cụ chat bot thông thường

#### Độ tin cậy và Chính xác:

- Để giảm ảo giác (Hallucination) của AI, bắt buộc phải phối hợp: Prompt Engineering + RAG + Fine-tuning
- Quy trình RAG chuẩn: $Input \rightarrow Embedding \rightarrow Context \rightarrow LLM \rightarrow Output$

### IV. KẾ HOẠCH ỨNG DỤNG VÀO CÔNG VIỆC

Dựa trên kiến thức đã học, tôi đề xuất các hướng ứng dụng cụ thể:

#### 1. Đối với dự án hiện tại

- **Tính năng:** Thử nghiệm tích hợp AI Agents vào quy trình Chăm sóc khách hàng (Customer Support) và Hỗ trợ đăng ký/đăng nhập
- **An toàn:** Áp dụng Bedrock Guardrails và các lớp validate để đảm bảo AI không trả lời các nội dung nhạy cảm hoặc sai lệch

#### 2. Đối với quy trình phát triển (Team & Learning)

- **Mô hình AI-DLC:** Phân chia rõ ràng nhiệm vụ: AI chịu trách nhiệm sinh mã nguồn (generate code) và viết tài liệu (docs); con người tập trung vào Review và Approve (phê duyệt)
- **Hạ tầng:** Cân nhắc kỹ lưỡng việc sử dụng Serverless (AWS Lambda) cho các tác vụ ngắn hạn so với Container (ECS/Fargate) cho các tác vụ dài hạn/phức tạp

#### 3. Định hướng cá nhân (Vai trò Intern/Developer)

- **Business-First:** Luôn đặt câu hỏi "Giá trị nghiệp vụ là gì?" trước khi viết code hoặc thu thập yêu cầu. Công nghệ phải phục vụ mục tiêu kinh doanh
- **Data Mindset:** Nhận thức rõ rằng một nền tảng dữ liệu sạch và có cấu trúc là điều kiện tiên quyết để GenAI hoạt động hiệu quả

### V. TRẢI NGHIỆM & ĐÁNH GIÁ

Điểm nhấn lớn nhất của sự kiện là workshop "GenAI-powered App-DB Modernization". Đây là cơ hội quý giá để thực hành hiện đại hóa cơ sở dữ liệu và ứng dụng.

- **Về chuyên môn:** Tôi đã hiểu rõ cách thiết kế một pipeline dữ liệu hoàn chỉnh và cách cân bằng giữa sức mạnh của AI với sự kiểm soát của con người (Human-in-the-loop)
- **Về công cụ:** Đã được tiếp cận thực tế với Amazon Bedrock, AgentCore và SageMaker Unified Studio
- **Về kết nối:** Việc trao đổi với các chuyên gia AWS giúp tôi mở rộng góc nhìn về các bài toán thực tế (Use cases) và cách giải quyết vấn đề ở quy mô doanh nghiệp

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của bạn tại đây

> **Tổng kết:** GenAI không chỉ là một công cụ, mà đòi hỏi một chiến lược tổng thể từ Dữ liệu, Bảo mật đến Kiến trúc. Việc áp dụng AI Agents và mô hình AI-DLC sẽ là chìa khóa để nâng cao năng suất và thay đổi cách vận hành hệ thống trong tương lai gần.
