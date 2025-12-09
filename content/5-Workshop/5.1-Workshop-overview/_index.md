---
title : "Workshop Overview"
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

## Introduction to EV Rental AI Agent

### What is an AI Agent?

An **AI Agent** is an intelligent system that can:
- Understand natural language queries
- Automatically select and execute appropriate tools/functions
- Make decisions based on context
- Provide structured responses with data

Unlike traditional chatbots with fixed responses, AI Agents can **reason** and **take actions** dynamically.



### System Architecture

Our EV Rental AI Agent uses a **multi-layered architecture**:

```
┌─────────────────┐
│  User Interface │  ← React Frontend (Chat UI)
└────────┬────────┘
         │ HTTP/REST
         ↓
┌─────────────────┐
│  FastAPI Server │  ← Backend Orchestrator
└────────┬────────┘
         │
    ┌────┴────────────────┐
    ↓                     ↓
┌──────────┐      ┌──────────────┐
│ Strands  │      │  PostgreSQL  │
│ Agent SDK│      │  (History)   │
└────┬─────┘      └──────────────┘
     │
     ├─────→ AWS Bedrock (Claude 3.5 Sonnet)
     ├─────→ Knowledge Base (Policies/FAQ)
     └─────→ Backend API (Vehicles/Stations)
```

<!-- ![System Architecture](/images/5-Workshop/5.1-Workshop-overview/image-1.png) -->

### Key Components

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **AI Model** | AWS Bedrock - Claude 3.5 Sonnet | Natural language understanding & generation |
| **Agent Framework** | Strands Agent SDK | Automatic tool selection & orchestration |
| **Backend API** | FastAPI (Python) | REST API server for agent logic |
| **Database** | PostgreSQL | Store chat history & sessions |
| **Frontend** | React + Chakra UI | Interactive chat interface |
| **Knowledge Base** | AWS Bedrock KB | Document retrieval (policies, FAQ) |

### Core Features

#### 1. **Knowledge Base Search**
Agent searches through uploaded documents to answer questions about:
- Rental policies
- Pricing information
- Booking procedures
- Terms and conditions

**Example Query:** 
> "Chính sách thuê xe của bạn là gì?"

**Agent Response:**
```markdown
## 📋 VinFast Rental Policies

### 📄 Required Documents:
- ✅ Valid ID/Passport
- ✅ Driver's License (Class B1+)
- ✅ Proof of Residence

### 💰 Pricing:
- **VF8**: 1,500,000 VNĐ/day
- **VF9**: 2,000,000 VNĐ/day
- **Deposit**: 10,000,000 VNĐ
```

#### 2. **Vehicle Search**
Agent queries the backend API to find available vehicles based on:
- Location (city)
- Date range
- Vehicle model/type

**Response Format:** Interactive vehicle cards with specs

#### 3. **Charging Station Finder**
Agent retrieves nearby charging stations with:
- Address and status
- Available chargers
- Distance (if location provided)

**Response Format:** Station cards with real-time availability

### Workshop Objectives

By the end of this workshop, you will be able to:

1. ✅ **Configure AWS Bedrock** - Enable Claude models and create a Knowledge Base
2. ✅ **Build an AI Agent Backend** - Use Strands SDK to orchestrate multiple tools
3. ✅ **Deploy a Chat Interface** - Create a responsive React chat UI
4. ✅ **Test End-to-End** - Interact with the AI agent and verify all functionalities

### Technology Stack

**AWS Services:**
- AWS Bedrock (Claude 3.5 Sonnet v2)
- AWS Bedrock Knowledge Bases
- AWS S3 (for document storage)
- IAM (for access management)

**Backend:**
- Python 3.11+
- FastAPI
- Strands Agent SDK
- PostgreSQL
- SQLAlchemy

**Frontend:**
- React 18
- Chakra UI
- Axios
- React Markdown

### Workshop Flow

```
Step 1: Prerequisites
   ↓
Step 2: Setup AWS Bedrock & Knowledge Base
   ↓
Step 3: Deploy Backend API (FastAPI)
   ↓
Step 4: Deploy Frontend (React)
   ↓
Step 5: Test the AI Agent
   ↓
Step 6: Cleanup Resources
```

---

**Next:** Let's move to [Prerequisites](../5.2-Prerequiste/) to prepare your environment.
