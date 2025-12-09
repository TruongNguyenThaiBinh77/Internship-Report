---
title: "Workshop"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Xây dựng EV Rental AI Agent với AWS Bedrock

#### Tổng quan

**EV Rental AI Agent** là một chatbot thông minh được xây dựng để hỗ trợ khách hàng trong hệ thống cho thuê xe điện VinFast. Workshop này hướng dẫn cách sử dụng **AWS Bedrock**, **Claude 3.5 Sonnet**, và **Knowledge Bases** để tạo một AI đàm thoại có thể:

- Trả lời câu hỏi tự nhiên bằng tiếng Việt
- Tự động tìm kiếm thông tin từ nhiều nguồn
- Hiển thị dữ liệu dưới dạng card tương tác trong giao diện chat
- Tra cứu xe khả dụng và trạm sạc
- Truy cập chính sách thuê xe và FAQ từ knowledge base

Trong workshop này, bạn sẽ học cách:
+ **Thiết lập AWS Bedrock** - Kích hoạt các AI model và tạo Knowledge Base để truy xuất tài liệu
+ **Triển khai Backend API** - Xây dựng FastAPI server với Strands Agent SDK cho việc chọn tool thông minh
+ **Triển khai Frontend** - Tạo giao diện chat React với các component Chakra UI
+ **Kiểm thử hệ thống** - Tương tác với AI agent và xác minh tất cả chức năng

#### Nội dung

1. [Tổng quan Workshop](5.1-Workshop-overview/)
2. [Yêu cầu chuẩn bị](5.2-Prerequiste/)
3. [Thiết lập AWS Bedrock](5.3-Setup-Bedrock/)
4. [Triển khai Backend API](5.4-Deploy-Backend/)
5. [Triển khai Frontend](5.5-Deploy-Frontend/)
6. [Kiểm thử AI Agent](5.6-Testing/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)
