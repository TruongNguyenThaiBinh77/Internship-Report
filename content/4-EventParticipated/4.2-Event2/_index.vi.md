---
title: "Event 2"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch "AWS Cloud Mastery Series #1: GENERATIVE AI, RAG & AWS AGENTIC AI"

---

### I. TỔNG QUAN SỰ KIỆN

**Tên sự kiện:** AWS Cloud Mastery Series #1: GENERATIVE AI, RAG & AWS AGENTIC AI

**Mục tiêu tham dự:**

1. Nắm bắt kỹ thuật Prompt Engineering và các dịch vụ AI có sẵn trên AWS
2. Tìm hiểu sâu về RAG (Retrieval-Augmented Generation) và ứng dụng trong doanh nghiệp
3. Cập nhật xu hướng Agentic AI và giải pháp đưa AI Agent từ thử nghiệm (POC) sang thực tế (Production)
4. Khám phá công nghệ Voice AI thời gian thực với Pipecat

**Danh Sách Diễn Giả:**

- **Lâm Tuấn Kiệt** - Sr DevOps Engineer (FPT Software)
- **Danh Hoàng Hiếu Nghị** - AI Engineer (Renova Cloud)
- **Đinh Lê Hoàng Anh** - Cloud Engineer Trainee (First Cloud AI Journey)

### II. NỘI DUNG KIẾN THỨC TRỌNG TÂM

Qua phần trình bày của các diễn giả từ FPT Software, Renova Cloud và First Cloud AI Journey, tôi đã tổng hợp được các nhóm kiến thức cốt lõi sau:

#### 1. Prompt Engineering & Foundation Models (Nền tảng cốt lõi)

Tôi đã củng cố được tư duy về cách giao tiếp với các Mô hình Nền tảng (Foundation Models) trên Amazon Bedrock. Điểm nhấn là sự khác biệt hiệu quả giữa:

- **Zero-shot / Few-shot Prompting:** Kỹ thuật điều hướng mô hình bằng chỉ dẫn trực tiếp hoặc cung cấp ví dụ mẫu
- **Chain of Thought (CoT):** Kỹ thuật yêu cầu mô hình "suy luận từng bước", giúp tăng đáng kể độ chính xác khi xử lý các vấn đề logic phức tạp

#### 2. Các Dịch vụ AWS AI Tiền huấn luyện (Pretrained Services)

Sự kiện đã hệ thống hóa lại các API "Ready-to-use" giúp tích hợp trí tuệ nhân tạo mà không cần huấn luyện mô hình lại từ đầu:

- **Hình ảnh/Video:** Amazon Rekognition
- **Ngôn ngữ & Văn bản:** Amazon Translate, Comprehend, Textract (OCR)
- **Âm thanh:** Amazon Polly (Text-to-Speech) và Transcribe (Speech-to-Text)

#### 3. RAG - Retrieval Augmented Generation

Đây là giải pháp quan trọng để giải quyết vấn đề "ảo giác" (hallucinations) của AI khi áp dụng vào doanh nghiệp. Quy trình được làm rõ thông qua:

- Sử dụng **Amazon Titan Text Embeddings V2** để vector hóa dữ liệu phục vụ tìm kiếm ngữ nghĩa
- Tận dụng **Knowledge Bases for Amazon Bedrock** để quản lý toàn trình từ khâu Chunking (chia nhỏ), lưu trữ Vector, đến Truy xuất và Tạo sinh câu trả lời

#### 4. Sự chuyển dịch sang Agentic AI & Thách thức Production

Tôi đã nắm bắt được sự tiến hóa từ **GenAI Assistants** (làm theo quy tắc) sang **GenAI Agents** (hướng mục tiêu, tự chủ). Tuy nhiên, việc chuyển đổi từ POC sang Production gặp rào cản lớn về:

- Hiệu suất và Khả năng mở rộng
- Bảo mật, Quản trị và Kiểm soát truy cập
- Sự phức tạp trong quản lý bộ nhớ và ngữ cảnh

#### 5. Giải pháp Amazon Bedrock AgentCore

Để giải quyết các thách thức trên, AWS giới thiệu AgentCore với các thành phần:

- **Runtime & Memory:** Môi trường thực thi và khả năng ghi nhớ lịch sử tương tác
- **Identity & Gateway:** Quản lý định danh và bảo mật
- **Code Interpreter:** Cho phép Agent viết và chạy code để xử lý dữ liệu phức tạp
- **Observability:** Công cụ giám sát và kiểm toán hành vi của Agent

#### 6. Pipecat Framework (Voice AI)

Một framework mã nguồn mở ấn tượng dành cho trợ lý ảo đa phương thức, hoạt động theo cơ chế pipeline thời gian thực: $WebRTC \rightarrow STT \rightarrow LLM \rightarrow TTS \rightarrow Output$.

---

### III. ĐÁNH GIÁ & BÀI HỌC KINH NGHIỆM

Sau khi tham gia workshop, tôi rút ra được 3 bài học và thay đổi trong tư duy quan trọng:

#### 1. Tư duy chuyển dịch từ "Hỏi - Đáp" sang "Hành động" (Agentic AI)

Trước đây, tôi thường giới hạn AI ở việc trò chuyện hoặc tóm tắt. Tuy nhiên, khái niệm **Agentic AI** đã mở ra viễn cảnh về những "nhân viên ảo" thực thụ. Khả năng lập kế hoạch và sử dụng công cụ (tool-use) của Agent là bước tiến lớn giúp tự động hóa các quy trình phức tạp mà không cần sự can thiệp liên tục của con người.

#### 2. Giải bài toán "Production" với AgentCore

Tôi rất tâm đắc với phần thảo luận về "Hố sâu ngăn cách" giữa POC và Production. Việc sử dụng các công cụ như **Amazon Bedrock AgentCore** không chỉ là vấn đề kỹ thuật mà là chìa khóa để xây dựng **niềm tin doanh nghiệp**. Các lớp bảo mật và kiểm soát (Observability) là yếu tố bắt buộc để doanh nghiệp dám giao việc cho AI.

#### 3. Tiềm năng ứng dụng thực tế của Pipecat

Sự kết hợp giữa WebRTC và AI Model của Pipecat tạo ra trải nghiệm hội thoại độ trễ cực thấp. Điều này gợi mở cho tôi nhiều ý tưởng ứng dụng thực tế như: tổng đài chăm sóc khách hàng thông minh, trợ lý phỏng vấn tuyển dụng, hoặc các ứng dụng luyện ngoại ngữ thời gian thực.

---

### IV. KẾT LUẬN

Workshop **"Generative AI & Agentic AI on AWS"** đã mang lại cái nhìn toàn cảnh và lộ trình công nghệ rõ ràng:

- **Hiện tại:** Tập trung làm chủ **RAG** và **Prompt Engineering**
- **Tương lai:** Hướng tới kỷ nguyên **Agentic AI** và các Tác tử tự chủ
- **Công cụ:** Tận dụng hệ sinh thái AWS (Bedrock, AgentCore) và các Framework như Pipecat để hiện thực hóa các ý tưởng đột phá

Workshop không chỉ cung cấp kiến thức lý thuyết mà còn trang bị cho tôi tầm nhìn thực tế về việc triển khai các giải pháp AI trong môi trường doanh nghiệp, đặc biệt là sự chuyển đổi từ các dự án thử nghiệm sang hệ thống sản xuất có tính bền vững và đáng tin cậy.

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của bạn tại đây

> Tổng thể, sự kiện đã giúp tôi mở rộng hiểu biết về xu hướng Generative AI và Agentic AI, đồng thời cung cấp công cụ và phương pháp luận cụ thể để áp dụng vào thực tế.
