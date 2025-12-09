---
title: "Event 2"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# Event Report "AWS Cloud Mastery Series #1: GENERATIVE AI, RAG & AWS AGENTIC AI"

---

### I. EVENT OVERVIEW

**Event Name:** AWS Cloud Mastery Series #1: GENERATIVE AI, RAG & AWS AGENTIC AI

**Objectives:**

1. Master Prompt Engineering techniques and available AI services on AWS
2. Deep dive into RAG (Retrieval-Augmented Generation) and its enterprise applications
3. Update on Agentic AI trends and solutions for moving AI Agents from Proof of Concept (POC) to Production
4. Explore real-time Voice AI technology with Pipecat

**Speaker List:**

- **Lam Tuan Kiet** - Sr DevOps Engineer (FPT Software)
- **Danh Hoang Hieu Nghi** - AI Engineer (Renova Cloud)
- **Dinh Le Hoang Anh** - Cloud Engineer Trainee (First Cloud AI Journey)

### II. KEY KNOWLEDGE INSIGHTS

Through presentations from speakers at FPT Software, Renova Cloud, and First Cloud AI Journey, I have compiled the following core knowledge groups:

#### 1. Prompt Engineering & Foundation Models (Core Foundation)

I consolidated my understanding of how to communicate with Foundation Models on Amazon Bedrock. The highlight is the effective difference between:

- **Zero-shot / Few-shot Prompting:** Techniques to guide the model through direct instructions or providing sample examples
- **Chain of Thought (CoT):** Technique requiring the model to "reason step by step", significantly increasing accuracy when handling complex logic problems

#### 2. AWS AI Pretrained Services

The event systematized "Ready-to-use" APIs that help integrate artificial intelligence without retraining models from scratch:

- **Image/Video:** Amazon Rekognition
- **Language & Text:** Amazon Translate, Comprehend, Textract (OCR)
- **Audio:** Amazon Polly (Text-to-Speech) and Transcribe (Speech-to-Text)

#### 3. RAG - Retrieval Augmented Generation

This is an important solution to address the "hallucinations" problem of AI when applied to enterprises. The process is clarified through:

- Using **Amazon Titan Text Embeddings V2** to vectorize data for semantic search
- Leveraging **Knowledge Bases for Amazon Bedrock** to manage the entire process from Chunking, Vector storage, to Retrieval and answer Generation

#### 4. Shift to Agentic AI & Production Challenges

I grasped the evolution from **GenAI Assistants** (rule-following) to **GenAI Agents** (goal-oriented, autonomous). However, the transition from POC to Production faces major obstacles:

- Performance and Scalability
- Security, Governance, and Access Control
- Complexity in memory and context management

#### 5. Amazon Bedrock AgentCore Solution

To address the above challenges, AWS introduces AgentCore with components:

- **Runtime & Memory:** Execution environment and ability to remember interaction history
- **Identity & Gateway:** Identity management and security
- **Code Interpreter:** Allows Agents to write and run code to process complex data
- **Observability:** Tools to monitor and audit Agent behavior

#### 6. Pipecat Framework (Voice AI)

An impressive open-source framework for multimodal virtual assistants, operating through real-time pipeline mechanism: $WebRTC \rightarrow STT \rightarrow LLM \rightarrow TTS \rightarrow Output$.

---

### III. EVALUATION & LESSONS LEARNED

After attending the workshop, I drew 3 important lessons and mindset changes:

#### 1. Mindset shift from "Q&A" to "Action" (Agentic AI)

Previously, I often limited AI to chatting or summarizing. However, the **Agentic AI** concept opened up a vision of true "virtual employees". The Agent's ability to plan and use tools is a major step forward helping automate complex processes without continuous human intervention.

#### 2. Solving the "Production" problem with AgentCore

I deeply appreciated the discussion about the "Deep gap" between POC and Production. Using tools like **Amazon Bedrock AgentCore** is not just a technical issue but the key to building **enterprise trust**. Security and control layers (Observability) are mandatory for enterprises to dare entrust work to AI.

#### 3. Real-world application potential of Pipecat

The combination of WebRTC and AI Model in Pipecat creates an extremely low-latency conversation experience. This opens up many practical application ideas for me such as: intelligent customer care hotline, recruitment interview assistant, or real-time language learning applications.

---

### IV. CONCLUSION

Workshop **"Generative AI & Agentic AI on AWS"** provided a comprehensive view and clear technology roadmap:

- **Present:** Focus on mastering **RAG** and **Prompt Engineering**
- **Future:** Towards the era of **Agentic AI** and autonomous Agents
- **Tools:** Leverage the AWS ecosystem (Bedrock, AgentCore) and Frameworks like Pipecat to realize breakthrough ideas

The workshop not only provided theoretical knowledge but also equipped me with practical vision on deploying AI solutions in enterprise environments, especially the transition from experimental projects to sustainable and reliable production systems.

#### Some images from the event
* Add your images here

> Overall, the event helped me expand my understanding of Generative AI and Agentic AI trends, while providing specific tools and methodologies to apply in practice.
