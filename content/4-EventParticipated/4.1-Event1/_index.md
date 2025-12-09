---
title: "Event 1"
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Event Report "Vietnam Cloud Day 2025: Ho Chi Minh City Connect Edition for Builders"

**Topic (Track 1):** GenAI & Data (Generative AI & Data)

### I. EVENT OBJECTIVES

The purpose of attending this event was to update on the latest trends and solutions on AWS, specifically focusing on 4 main objectives:

1. **Comprehensive GenAI Strategy:** Understanding how to build AI-driven software development lifecycle (AI-DLC) and the latest GenAI strategies
2. **Enterprise Security:** Deep understanding of security in GenAI and AI Agents to ensure data safety
3. **Data Foundation:** Learning how to build a Unified Data Foundation optimized for Analytics and AI
4. **Expert Connection:** Direct interaction with engineers and experts from AWS

**Speakers:**

AWS Team: Jun Kai Loke (AI/ML Specialist), Kien Nguyen, Tamelly Lim, Binh Tran, Taiki Dang (Solutions Architects), Michael Armentano (Principal WW GTM Specialist).

### II. KEY TECHNICAL INSIGHTS

#### 1. Unified Data Platform

For AI to operate effectively, data needs to be processed seamlessly. AWS emphasizes the Zero-ETL model and breaking down data "silos":

- **End-to-End Process:** From Ingestion $\rightarrow$ Storage $\rightarrow$ Processing $\rightarrow$ Access $\rightarrow$ Governance
- **Service Ecosystem:** Tight integration between Amazon S3, Glue, Redshift, Lake Formation, and OpenSearch
- **Self-service Mindset:** Empowering project teams to extract data autonomously while ensuring compliance with common standards

#### 2. GenAI Strategy & Amazon Bedrock

- **Amazon Bedrock:** Plays a central role in selecting Foundation Models, implementing RAG (Retrieval-Augmented Generation), and optimizing cost/latency
- **AgentCore & Amazon Nova:** Strongly supports modern Agent frameworks like CrewAI, LangGraph, LlamaIndex, helping build complex automation tasks

#### 3. Multi-layer Security for GenAI (Securing GenAI)

Security is not only at the infrastructure level but must be applied following the "Defense in Depth" model:

- **3 Security Layers:** Infrastructure $\rightarrow$ Model $\rightarrow$ Application
- **5 Main Pillars:** Compliance, Privacy, Controls, Risk Management, and Resilience
- **Practical Tools:** Using Bedrock Guardrails to review input/output content and OpenTelemetry for Observability

#### 4. AI-Driven Development Lifecycle (AI-DLC)

This is an important shift in software development thinking:

- **Evolution:** Shifting from AI-Assisted (AI supports code) $\rightarrow$ AI-Driven (AI leads) $\rightarrow$ AI-Managed (AI manages operations)
- **Implementation:** Integrating AI into all stages: from IaC (Infrastructure as Code), Automated Testing to risk management

#### 5. Amazon SageMaker – Unified Studio

- Unified environment for Data, Analytics, and AI, supporting Lakehouse architecture
- Comprehensive MLOps integration (Pipelines, Registry, Monitoring) helps accelerate bringing GenAI applications to market

### III. LESSONS LEARNED & KEY INSIGHTS

From the above content, I have drawn 3 core lessons for project development:

#### Design Mindset:

- Need to build Data & AI systems with an "End-to-End" mindset from the start, avoiding fragmentation
- Governance principles must go hand in hand with Self-service capability

#### Technical Architecture:

- Maximize Zero-ETL (integrate S3 $\leftrightarrow$ Redshift/Aurora/DynamoDB) to minimize data pipeline operational effort
- Use AI Agents to automate processes instead of just using AI as a regular chatbot tool

#### Reliability and Accuracy:

- To reduce AI Hallucination, must combine: Prompt Engineering + RAG + Fine-tuning
- Standard RAG process: $Input \rightarrow Embedding \rightarrow Context \rightarrow LLM \rightarrow Output$

### IV. ACTION PLAN FOR WORK APPLICATION

Based on the knowledge learned, I propose specific application directions:

#### 1. For current projects

- **Features:** Experiment with integrating AI Agents into Customer Support processes and Registration/Login support
- **Safety:** Apply Bedrock Guardrails and validation layers to ensure AI does not respond with sensitive or incorrect content

#### 2. For development processes (Team & Learning)

- **AI-DLC Model:** Clearly divide tasks: AI is responsible for generating source code and writing documentation; humans focus on Review and Approve
- **Infrastructure:** Carefully consider using Serverless (AWS Lambda) for short-term tasks versus Container (ECS/Fargate) for long-term/complex tasks

#### 3. Personal direction (Intern/Developer role)

- **Business-First:** Always ask "What is the business value?" before writing code or gathering requirements. Technology must serve business objectives
- **Data Mindset:** Recognize that a clean and structured data platform is a prerequisite for GenAI to operate effectively

### V. EXPERIENCE & EVALUATION

The biggest highlight of the event was the workshop "GenAI-powered App-DB Modernization". This was a valuable opportunity to practice modernizing databases and applications.

- **Professionally:** I clearly understood how to design a complete data pipeline and how to balance AI power with human control (Human-in-the-loop)
- **Tools:** Had practical exposure to Amazon Bedrock, AgentCore, and SageMaker Unified Studio
- **Connections:** Interacting with AWS experts helped me broaden my perspective on real-world problems (Use cases) and how to solve problems at enterprise scale

#### Some images from the event
* Add your images here

> **Summary:** GenAI is not just a tool, but requires a comprehensive strategy from Data, Security to Architecture. Applying AI Agents and the AI-DLC model will be the key to improving productivity and changing how systems are operated in the near future.
