---
title: "Proposal"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

📄 **[View Full Proposal Document (Google Docs)](https://docs.google.com/document/d/1VeR7Leu9Yq4LMlgPcfKtcE0IfO-K-DO4fgaWR8af7t0/edit?tab=t.0)**

---

# The EV Station-based Rental System

## Electric Vehicle Rental and Return Software at Fixed Stations – A Green Mobility Solution for Smart Cities

### 1. Executive Summary

The EV Station-based Rental System is developed to provide an all-in-one platform for electric vehicle rental and charging management. It integrates real-time rental, payment, and charging station access through a unified cloud-native solution. The system features a React Native mobile app and a Spring Boot backend deployed on AWS ECS Fargate, with PostgreSQL (RDS) and Redis (ElastiCache) for data and caching. User authentication is managed via Amazon Cognito, and global delivery is optimized using CloudFront. Designed under the AWS Well-Architected Framework, the platform ensures scalability, high availability, and security while maintaining cost efficiency.

### 2. Problem Statement

### What’s the Problem?

Current electric vehicle (EV) rental services are fragmented, requiring users to switch between multiple apps to locate, book, and manage rentals at fixed points. This creates inconvenience, slow performance, and unreliable experiences — users often arrive at “unavailable” or “offline” rental points, leading to frustration and loss of trust.

For vehicle owners and operators, manual fleet management, booking coordination, and maintenance tracking result in operational inefficiencies and lost revenue. Currently, there is no unified, real-time platform connecting renters, vehicle owners, and rental point operators.

### The Solution

The EV Station-based Rental System consolidates EV rental and return at fixed points into a single, cloud-native platform. Built with React Native for mobile and Spring Boot for backend, the system delivers real-time booking, vehicle tracking, and payment integration.

Key AWS services include ECS Fargate for compute, RDS PostgreSQL for data storage, ElastiCache for low-latency performance, API Gateway and Cognito for secure access, and CloudFront for global content delivery. The platform supports both fleet-based and peer-to-peer (P2P) vehicle registration, providing a centralized interface for users and operators to manage rentals efficiently, securely, and at scale.

### Benefits and Return on Investment

The platform eliminates manual coordination and fragmented applications, offering a unified, automated experience for renters and fleet owners. Real-time data ensures reliability and transparency regarding vehicle availability and rental point status.

Designed under the AWS Well-Architected Framework, the system minimizes operational costs with a serverless, pay-per-use model while maintaining scalability and 99.99% uptime. Within 12–24 months, the platform is projected to reach 50,000+ monthly active users, onboard 200+ rental points, and deliver significant time, cost, and operational efficiencies for both users and operators.

### 3. Solution Architecture

The VoltGo platform adopts a serverless and fully private AWS architecture for secure and scalable backend operations. Backend run on Amazon ECS Fargate, connecting to Aurora PostgreSQL Serverless v2 for relational data and ElastiCache Serverless (Redis) for caching.
All workloads are deployed in private subnets across multiple Availability Zones and accessed securely through API Gateway via AWS PrivateLink to an internal Network Load Balancer. User authentication is managed by Amazon Cognito, while the frontend is hosted on Amazon S3 and delivered globally via CloudFront, protected by AWS WAF and ACM SSL/TLS.
Monitoring and secrets management are handled by CloudWatch and Secrets Manager, with the entire infrastructure provisioned through Terraform IaC. This architecture ensures high security, elasticity, and cost efficiency suitable for the current development stage and future production scaling.

![IoT Weather Station Architecture](/images/2-Proposal/edge_architecture.jpeg)

### AWS Services Used

- **Amazon ECS Fargate**: Serverless container orchestration for backend microservices.
- **Amazon Aurora PostgreSQL Serverless v2**: Scalable, multi-AZ relational database.
- **Amazon ElastiCache Serverless (Redis)**: In-memory caching for low-latency data access.
- **Amazon API Gateway**: Secure REST API entry point integrated via PrivateLink.
- **Amazon Cognito**: User authentication and authorization with JWT and MFA.
- **Amazon CloudFront + S3**: Global content delivery and static hosting with WAF protection.
- **AWS Secrets Manager**: Centralized secret storage and automatic rotation.
- **Amazon CloudWatch**: Unified monitoring, logging, and alerting for all services.
- **AWS WAF + ACM**: Edge-level security and SSL/TLS certificate management.

### Component Design

- **Frontend**:React/Vue.js web application hosted on Amazon S3 and delivered via CloudFront, secured with AWS WAF and ACM SSL/TLS certificates.
- **API Layer**: Amazon API Gateway provides the public API endpoint, connecting privately to backend services through AWS PrivateLink to an internal Network Load Balancer.
- **Compute Layer**: Amazon ECS Fargate runs containerized microservices across multiple Availability Zones, scaling automatically based on CPU and memory utilization.
- **Database Layer**:Amazon Aurora PostgreSQL Serverless v2 stores relational data with a writer and read replica for high availability and automated scaling.
- **Caching Layer**: Amazon ElastiCache Serverless (Redis) caches session and booking data to reduce database load and improve response time.
- **Authentication**: Amazon Cognito handles user registration, login, and JWT-based authorization with optional MFA support.
- **Storage**: Amazon S3 manages static assets and user uploads, accessible only through CloudFront via Origin Access Control (OAC).
- **Monitoring & Security**: Amazon CloudWatch tracks logs and performance metrics, while AWS Secrets Manager securely stores credentials with automatic rotation.

### 4. Technical Implementation

**Implementation Phases**
This project has two main parts—developing the backend locally and deploying it to the AWS cloud—each following four key phases:

- 1.Build and Design Architecture:
  Develop and test backend services locally using Docker Compose, PostgreSQL, and Redis. Design the AWS serverless architecture including ECS Fargate, Aurora Serverless, ElastiCache, and API Gateway with PrivateLink connections. (Pre-deployment phase)
- 2.Estimate Cost and Validate Feasibility:
  Use AWS Pricing Calculator to estimate the monthly cost of ECS tasks, Aurora capacity units, and CloudFront bandwidth. Adjust design decisions to ensure cost-effectiveness and smooth migration.
- 3.Configure and Deploy Infrastructure:
  Build and deploy cloud infrastructure using Terraform for IaC. Configure VPC, ECS, Aurora, ElastiCache, Cognito, and CloudFront. Validate IAM roles, networking, and private-only access via VPC Endpoints.
- 4.Test, Optimize, and Release:
  Deploy Dockerized services to ECS Fargate, test API Gateway → PrivateLink → NLB → ECS flow, and verify database connections. Enable CloudWatch monitoring, auto-scaling, and WAF protection. Optimize scaling thresholds and document final architecture.

**Technical Requirements**

- Backend Services:
  Node.js or Spring Boot microservices for Auth, Booking, and Payment, containerized with Docker and deployed to ECS Fargate (2–10 tasks, auto-scaling).
- Database Layer:
  Amazon Aurora PostgreSQL Serverless v2 with writer and reader instances, supporting automatic scaling and multi-AZ high availability.
- Caching Layer:
  Amazon ElastiCache Serverless (Redis 7.1) for session caching and frequently accessed data.
- Authentication:
  Amazon Cognito manages user registration, JWT-based authentication, and optional MFA, integrated with API Gateway.
- Storage & Content Delivery:
  Frontend hosted on Amazon S3 and distributed via CloudFront, protected by AWS WAF and ACM SSL/TLS certificates.
- Secrets & Monitoring:
  AWS Secrets Manager for storing credentials (DB, Redis, JWT keys) with 30-day rotation. Amazon CloudWatch for logging, metrics, and scaling alarms.

### 5. Timeline & Milestones

**Project Timeline**

- Phase 1: Foundation & Design (Weeks 1-2)
  - Week 1: Finalize MVP scope (P0 User Stories), define user flows, and approve the AWS architecture.
  - Week 2: FE Lead finalizes UI/UX mockups. Backend provisions core AWS (VPC, S3, ECR, Aurora).
- Phase 2: Core MVP Development (Weeks 3-8)
  - Weeks 3-4: Backend builds User Auth (Cognito) & core APIs (API Gateway, ECS).
  - Weeks 5-6: All teams (FE/BE/Mobile) build core screens (Login, Search, Details) and the Booking Engine APIs.
  - Weeks 7-8: Integration of KYC flow (Lambda, Textract, Rekognition) and Payment Gateway integration.
- Phase 3: Testing & UAT (Weeks 9-10)
  - Week 9: Full End-to-End (E2E) testing. QA is performed by the 5-person dev team, as no dedicated QA is allocated.
  - Week 10: Stakeholder User Acceptance Testing (UAT) and final critical bug fixing.
- Phase 4: Launch (Week 11)
  - Week 11: Production deployment, Go-live, and intensive Hypercare monitoring via CloudWatch.

### 6. Budget Estimation

This budget estimate is based on the provided AWS architecture diagram and the "cheapest possible" MVP launch strategy, maximizing Free Tier usage.

### Infrastructure Costs

- AWS Services (Monthly Estimate):
  - Amazon Route 53: $0.50/month (1 hosted zone).
  - AWS WAF: $6.00/month (1 WebACL + 1 Rule + minimal requests).
  - AWS S3 Standard: $0.00/month (Stays within 5GB Always Free tier).
  - Amazon CloudFront: $0.00/month (Stays within 1TB/10M request Always Free tier).
  - AWS Cognito: $0.00/month (Stays within 10,000 MAU free tier).
  - Amazon API Gateway: $0.00/month (Stays within 1M request 12-month free tier).
  - AWS Lambda: $0.00/month (Stays within 1M request Always Free tier).
  - Amazon Textract/Rekognition: $0.00/month (Stays within 12-month free tier for KYC).
  - Application Load Balancer: $17.52/month (1 ALB, minimal processing).
  - VPC Endpoint (PrivateLink): $7.30/month (1 Endpoint, 1 AZ, 1GB data).
  - Amazon ECS on Fargate: ~$20.00/month (Assumes 2 minimal 24/7 containers, e.g., 0.25 vCPU/0.5GB RAM).
  - Amazon Aurora Serverless v2: ~$25.00/month (Minimal ACUs, configured to scale to near-zero).
  - Amazon ElastiCache Serverless: ~$10.00/month (Minimal usage).
  - Amazon CloudWatch: $0.00/month (Stays within 5GB log Always Free tier).
  - Amazon ECR: ~$0.10/month (Minimal storage over 500MB free tier).

Total: ~$86.42/month, ~$1,037.04/12 months

### 7. Risk Assessment

#### Risk Matrix

- System Downtime: High impact, medium probability.
- Data Sync Errors (Between Stations & Server): Medium impact, high probability.
- OCR Verification Failure: Medium impact, medium probability.
- Vehicle Shortage or Low Battery at Stations: High impact, high probability.
- Operational Mistakes by Staff: Medium impact, medium probability.
- Cost Overruns: Medium impact, low probability.

#### Mitigation Strategies

- System: Use load-balanced cloud servers with auto-scaling and failover backup.
- Data Sync: Implement offline caching and periodic background synchronization.
- OCR Verification: Combine AI-based ID recognition with manual approval option.
- Vehicle Management: Real-time tracking of battery and vehicle status; predictive restocking via analytics.
- Staff Operations: Provide training and digital checklists to reduce human error.
- Cost: Set up cloud cost monitoring and optimization alerts.

#### Contingency Plans

- Enable offline mode for station staff when Internet is unavailable.
- Activate backup servers in case of major downtime.
- Provide manual check-in/out workflow for rentals during system outages.
- Deploy mobile maintenance team to handle vehicle or battery issues at stations.
- Suspend or limit reservations dynamically if vehicle supply falls below safe threshold.

### 8. Expected Outcomes

#### Technical Improvements:

- Real-time monitoring of all EV stations and rental status.
- Automated verification and e-contract signing replace manual paperwork.
- Centralized dashboard for admins to manage fleet, customers, and staff.
- System scalable to 20+ rental stations in the next deployment phase.

#### Long-term Value

- Establishes a reliable EV mobility infrastructure for urban areas.
- Builds data foundation for future AI-powered demand forecasting.
- Enables integration with smart city and green transportation networks.
- Serves as a reusable platform for expanding to nationwide EV-sharing projects.

#### Short to Medium-term Benefits

- Faster customer onboarding (from 15 mins → <5 mins).
- Increased fleet utilization rate by 30% through data-driven scheduling.
- Improved accuracy of rental records and payment reconciliation.
- Enhanced user satisfaction via seamless booking and transparent billing.
