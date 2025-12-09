---
title : "Triển khai Backend API"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Triển khai Backend API với FastAPI

Trong phần này, bạn sẽ thiết lập máy chủ backend FastAPI điều phối AI agent sử dụng Strands SDK.

### Bước 1: Clone hoặc Tạo Cấu trúc Dự án

Tạo thư mục mới cho backend:

```bash
mkdir ev-rental-backend
cd ev-rental-backend
```

**Cấu trúc dự án:**
```
ev-rental-backend/
├── app/
│   ├── __init__.py
│   ├── main.py           # Ứng dụng FastAPI
│   ├── agent.py          # Thiết lập Strands Agent
│   ├── tools.py          # Công cụ Agent (tìm xe, trạm)
│   └── database.py       # Kết nối PostgreSQL
├── requirements.txt      # Thư viện Python
├── .env                  # Biến môi trường
└── README.md
```

![Cấu trúc Backend](/images/5-Workshop/5.4-Deploy-Backend/image-7.png)

### Bước 2: Cài đặt Thư viện

Tạo file `requirements.txt`:

```txt
fastapi==0.104.1
uvicorn[standard]==0.24.0
strands-agent-sdk==0.1.5
boto3==1.34.10
psycopg2-binary==2.9.9
sqlalchemy==2.0.23
pydantic==2.5.2
python-dotenv==1.0.0
httpx==0.25.2
```

**Cài đặt các thư viện:**
```bash
# Tạo môi trường ảo
python -m venv venv

# Kích hoạt môi trường ảo
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Cài đặt packages
pip install -r requirements.txt
```

### Bước 3: Cấu hình Biến Môi trường

Tạo file `.env` với thông tin AWS và Knowledge Base ID:

```env
# AWS Credentials
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY
AWS_REGION=us-west-2

# Cấu hình Bedrock
BEDROCK_MODEL_ID=anthropic.claude-3-5-sonnet-20241022-v2:0
KNOWLEDGE_BASE_ID=89CI1JSSE4

# Cấu hình Database
DATABASE_URL=postgresql://postgres:password@localhost:5432/ev_rental_db

# Cấu hình API
BACKEND_API_URL=http://localhost:8080
```

**⚠️ Lưu ý Bảo mật:** 
- Không bao giờ commit `.env` lên Git
- Thêm `.env` vào `.gitignore`

![Cấu hình Môi trường](/images/5-Workshop/5.4-Deploy-Backend/image-8.png)

### Bước 4: Tạo Database Models

Tạo file `app/database.py`:

```python
from sqlalchemy import create_engine, Column, Integer, String, Text, DateTime
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker
from datetime import datetime
import os

DATABASE_URL = os.getenv("DATABASE_URL")

engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
Base = declarative_base()

class ChatHistory(Base):
    __tablename__ = "chat_history"
    
    id = Column(Integer, primary_key=True, index=True)
    session_id = Column(String, index=True)
    user_message = Column(Text)
    agent_response = Column(Text)
    timestamp = Column(DateTime, default=datetime.utcnow)

# Tạo bảng
Base.metadata.create_all(bind=engine)
```

### Bước 5: Tạo Agent Tools

Tạo file `app/tools.py`:

```python
import httpx
import os
from typing import List, Dict

BACKEND_API_URL = os.getenv("BACKEND_API_URL", "http://localhost:8080")

async def search_vehicles(location: str = None, model: str = None) -> List[Dict]:
    """Tìm kiếm xe có sẵn"""
    async with httpx.AsyncClient() as client:
        params = {}
        if location:
            params["location"] = location
        if model:
            params["model"] = model
        
        response = await client.get(f"{BACKEND_API_URL}/api/vehicles", params=params)
        return response.json()

async def search_stations(city: str = None) -> List[Dict]:
    """Tìm kiếm trạm sạc"""
    async with httpx.AsyncClient() as client:
        params = {}
        if city:
            params["city"] = city
        
        response = await client.get(f"{BACKEND_API_URL}/api/stations", params=params)
        return response.json()
```

### Bước 6: Thiết lập Strands Agent

Tạo file `app/agent.py`:

```python
import boto3
import os
from strands_agent import Agent, Tool

# Khởi tạo Bedrock client
bedrock_client = boto3.client(
    'bedrock-runtime',
    region_name=os.getenv('AWS_REGION'),
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY_ID'),
    aws_secret_access_key=os.getenv('AWS_SECRET_ACCESS_KEY')
)

# Khởi tạo Knowledge Base client
bedrock_agent_client = boto3.client(
    'bedrock-agent-runtime',
    region_name=os.getenv('AWS_REGION'),
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY_ID'),
    aws_secret_access_key=os.getenv('AWS_SECRET_ACCESS_KEY')
)

# Tạo Agent
agent = Agent(
    model_id=os.getenv('BEDROCK_MODEL_ID'),
    client=bedrock_client,
    knowledge_base_id=os.getenv('KNOWLEDGE_BASE_ID'),
    tools=[
        Tool(
            name="search_vehicles",
            description="Tìm kiếm xe điện có sẵn để thuê",
            function=search_vehicles
        ),
        Tool(
            name="search_stations",
            description="Tìm trạm sạc gần đó",
            function=search_stations
        )
    ]
)
```

### Bước 7: Tạo Ứng dụng FastAPI

Tạo file `app/main.py`:

```python
from fastapi import FastAPI, HTTPException
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
from app.agent import agent
from app.database import SessionLocal, ChatHistory
import uuid

app = FastAPI(title="EV Rental AI Agent API")

# Bật CORS
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

class ChatRequest(BaseModel):
    message: str
    session_id: str = None

class ChatResponse(BaseModel):
    response: str
    session_id: str
    data: dict = None

@app.post("/chat", response_model=ChatResponse)
async def chat(request: ChatRequest):
    try:
        # Tạo session ID nếu chưa có
        session_id = request.session_id or str(uuid.uuid4())
        
        # Lấy phản hồi từ agent
        agent_response = await agent.run(request.message)
        
        # Lưu vào database
        db = SessionLocal()
        chat_record = ChatHistory(
            session_id=session_id,
            user_message=request.message,
            agent_response=agent_response["response"]
        )
        db.add(chat_record)
        db.commit()
        db.close()
        
        return ChatResponse(
            response=agent_response["response"],
            session_id=session_id,
            data=agent_response.get("data")
        )
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))

@app.get("/health")
async def health_check():
    return {"status": "healthy"}
```

### Bước 8: Chạy Backend Server

Khởi động máy chủ FastAPI:

```bash
# Đảm bảo môi trường ảo đã được kích hoạt
uvicorn app.main:app --reload --port 8000

# Bạn sẽ thấy:
# INFO:     Uvicorn running on http://127.0.0.1:8000
# INFO:     Application startup complete.
```

![Backend Đang Chạy](/images/5-Workshop/5.4-Deploy-Backend/image-9.png)

### Bước 9: Kiểm tra API

**Kiểm tra endpoint health:**
```bash
curl http://localhost:8000/health
# Kết quả: {"status":"healthy"}
```

**Kiểm tra endpoint chat:**
```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Chính sách thuê xe của bạn là gì?"}'
```

**Kết quả mong đợi:**
```json
{
  "response": "## 📋 Chính sách thuê xe VinFast\n\n### 📄 Giấy tờ cần thiết:\n- CMND/CCCD...",
  "session_id": "abc123-...",
  "data": null
}
```

### Checklist Xác minh

Trước khi tiếp tục, đảm bảo:

- ✅ Môi trường ảo đã được tạo và kích hoạt
- ✅ Tất cả thư viện đã được cài đặt
- ✅ File `.env` đã được cấu hình với AWS credentials
- ✅ PostgreSQL database đang chạy và kết nối được
- ✅ Máy chủ FastAPI đang chạy trên cổng 8000
- ✅ Endpoint health check trả về `{"status":"healthy"}`
- ✅ Endpoint chat trả về phản hồi hợp lệ

### Xử lý Sự cố

**Vấn đề: "ModuleNotFoundError"**
- Giải pháp: Đảm bảo môi trường ảo đã được kích hoạt và thư viện đã cài đặt

**Vấn đề: "Database connection failed"**
- Kiểm tra PostgreSQL đang chạy
- Xác minh DATABASE_URL trong `.env`
- Test kết nối: `psql -h localhost -U postgres -d ev_rental_db`

**Vấn đề: "Bedrock ValidationException"**
- Xác minh AWS credentials trong `.env`
- Đảm bảo quyền truy cập model đã được cấp trong Bedrock console
- Kiểm tra KNOWLEDGE_BASE_ID chính xác

---

**Tiếp theo:** Chuyển sang [Triển khai Frontend](../5.5-Deploy-Frontend/) để tạo giao diện chat React.
