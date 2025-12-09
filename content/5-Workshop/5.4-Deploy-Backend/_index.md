---
title : "Deploy Backend API"
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

## Deploy Backend API with FastAPI

In this section, you will set up the FastAPI backend server that orchestrates the AI agent using Strands SDK.

### Step 1: Clone or Create Project Structure

Create a new directory for the backend:

```bash
mkdir ev-rental-backend
cd ev-rental-backend
```

**Project structure:**
```
ev-rental-backend/
├── app/
│   ├── __init__.py
│   ├── main.py           # FastAPI app
│   ├── agent.py          # Strands Agent setup
│   ├── tools.py          # Agent tools (search vehicles, stations)
│   └── database.py       # PostgreSQL connection
├── requirements.txt      # Python dependencies
├── .env                  # Environment variables
└── README.md
```


### Step 2: Install Dependencies

Create `requirements.txt`:

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

**Install dependencies:**
```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install packages
pip install -r requirements.txt
```

### Step 3: Configure Environment Variables

Create `.env` file with your AWS credentials and Knowledge Base ID:

```env
# AWS Credentials
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY
AWS_REGION=us-west-2

# Bedrock Configuration
BEDROCK_MODEL_ID=anthropic.claude-3-5-sonnet-20241022-v2:0
KNOWLEDGE_BASE_ID=89CI1JSSE4

# Database Configuration
DATABASE_URL=postgresql://postgres:password@localhost:5432/ev_rental_db

# API Configuration
BACKEND_API_URL=http://localhost:8080
```

**⚠️ Security Note:** 
- Never commit `.env` to Git
- Add `.env` to `.gitignore`


### Step 4: Create Database Models

Create `app/database.py`:

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

# Create tables
Base.metadata.create_all(bind=engine)
```

### Step 5: Create Agent Tools

Create `app/tools.py`:

```python
import httpx
import os
from typing import List, Dict

BACKEND_API_URL = os.getenv("BACKEND_API_URL", "http://localhost:8080")

async def search_vehicles(location: str = None, model: str = None) -> List[Dict]:
    """Search for available vehicles"""
    async with httpx.AsyncClient() as client:
        params = {}
        if location:
            params["location"] = location
        if model:
            params["model"] = model
        
        response = await client.get(f"{BACKEND_API_URL}/api/vehicles", params=params)
        return response.json()

async def search_stations(city: str = None) -> List[Dict]:
    """Search for charging stations"""
    async with httpx.AsyncClient() as client:
        params = {}
        if city:
            params["city"] = city
        
        response = await client.get(f"{BACKEND_API_URL}/api/stations", params=params)
        return response.json()
```

### Step 6: Setup Strands Agent

Create `app/agent.py`:

```python
import boto3
import os
from strands_agent import Agent, Tool

# Initialize Bedrock client
bedrock_client = boto3.client(
    'bedrock-runtime',
    region_name=os.getenv('AWS_REGION'),
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY_ID'),
    aws_secret_access_key=os.getenv('AWS_SECRET_ACCESS_KEY')
)

# Initialize Knowledge Base client
bedrock_agent_client = boto3.client(
    'bedrock-agent-runtime',
    region_name=os.getenv('AWS_REGION'),
    aws_access_key_id=os.getenv('AWS_ACCESS_KEY_ID'),
    aws_secret_access_key=os.getenv('AWS_SECRET_ACCESS_KEY')
)

# Create Agent
agent = Agent(
    model_id=os.getenv('BEDROCK_MODEL_ID'),
    client=bedrock_client,
    knowledge_base_id=os.getenv('KNOWLEDGE_BASE_ID'),
    tools=[
        Tool(
            name="search_vehicles",
            description="Search for available electric vehicles for rent",
            function=search_vehicles
        ),
        Tool(
            name="search_stations",
            description="Find nearby charging stations",
            function=search_stations
        )
    ]
)
```

### Step 7: Create FastAPI Application

Create `app/main.py`:

```python
from fastapi import FastAPI, HTTPException
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
from app.agent import agent
from app.database import SessionLocal, ChatHistory
import uuid

app = FastAPI(title="EV Rental AI Agent API")

# Enable CORS
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
        # Generate session ID if not provided
        session_id = request.session_id or str(uuid.uuid4())
        
        # Get agent response
        agent_response = await agent.run(request.message)
        
        # Save to database
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

### Step 8: Run the Backend Server

Start the FastAPI server:

```bash
# Make sure virtual environment is activated
uvicorn app.main:app --reload --port 8000

# You should see:
# INFO:     Uvicorn running on http://127.0.0.1:8000
# INFO:     Application startup complete.
```


### Step 9: Test the API

**Test health endpoint:**
```bash
curl http://localhost:8000/health
# Response: {"status":"healthy"}
```

**Test chat endpoint:**
```bash
curl -X POST http://localhost:8000/chat \
  -H "Content-Type: application/json" \
  -d '{"message": "Chính sách thuê xe của bạn là gì?"}'
```

**Expected response:**
```json
{
  "response": "## 📋 Chính sách thuê xe VinFast\n\n### 📄 Giấy tờ cần thiết:\n- CMND/CCCD...",
  "session_id": "abc123-...",
  "data": null
}
```

### Verification Checklist

Before proceeding, ensure:

- ✅ Virtual environment created and activated
- ✅ All dependencies installed
- ✅ `.env` file configured with AWS credentials
- ✅ PostgreSQL database running and connected
- ✅ FastAPI server running on port 8000
- ✅ Health check endpoint returns `{"status":"healthy"}`
- ✅ Chat endpoint returns proper responses

### Troubleshooting

**Issue: "ModuleNotFoundError"**
- Solution: Ensure virtual environment is activated and dependencies installed

**Issue: "Database connection failed"**
- Check PostgreSQL is running
- Verify DATABASE_URL in `.env`
- Test connection: `psql -h localhost -U postgres -d ev_rental_db`

**Issue: "Bedrock ValidationException"**
- Verify AWS credentials in `.env`
- Ensure model access is granted in Bedrock console
- Check KNOWLEDGE_BASE_ID is correct

---

**Next:** Proceed to [Deploy Frontend](../5.5-Deploy-Frontend/) to create the React chat interface.
