---
title: "Event 3"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

# Event Report "AWS Cloud Mastery Series #2: From DevOps, IaC to Containers & Observability"

### I. EVENT OVERVIEW

**Event Name:** AWS Cloud Mastery Series #2: From DevOps, IaC to Containers & Observability

**Objectives:**

1. **Mindset Standardization:** Deep understanding of Value Cycle and the core role of DevOps
2. **Infrastructure Modernization (IaC):** Transition from manual operations (ClickOps) to Infrastructure as Code
3. **Application Optimization (Containerization):** Master the strategy of choosing appropriate container platforms (App Runner, ECS, EKS)
4. **Comprehensive Observability:** Build proactive monitoring systems with CloudWatch and X-Ray

**Speaker List:**

AWS Experts & Cloud Engineers Team: Sharing about system architecture, Platform Engineering strategy, and in-depth technical demos.

### II. KEY KNOWLEDGE INSIGHTS

Through sharing from AWS experts and Cloud engineers, I have distilled the following foundational knowledge blocks:

#### 1. DevOps Mindset & CI/CD Pipeline

The event began by redefining DevOps not just as tools, but as a culture of optimizing value flow.

**Value Cycle:** A closed-loop 5-step process aimed at increasing delivery Speed while ensuring Stability.

**Effective Pipeline Strategy:**

Clearly distinguish Concepts:
- **Continuous Integration (CI):** Fail fast, integrate code daily
- **Continuous Delivery:** Automate to Staging, requires human approval for Production
- **Continuous Deployment:** 100% automation to Production

**"Build Once, Deploy Anywhere" Principle:** Source code is built only once into a Binary package (Artifact). Subsequent environments (Staging, Prod) reuse this same Artifact to ensure absolute consistency.

**Fail Fast Conditions:** Pipeline must stop immediately when encountering compilation errors, Code Style violations, security vulnerabilities, or slow tests.

#### 2. Infrastructure as Code (IaC) - From ClickOps to Code

This section addresses the problem of eliminating manual operations ("ClickOps") that are error-prone and difficult to scale. I analyzed 3 main tools in depth:

**AWS CloudFormation (Native):**
- Uses YAML/JSON
- Manages resources in Stack units
- Deleting a Stack means deleting all related resources

**Terraform (Multi-Cloud):**
- Uses HCL language
- Strength is multi-platform support
- Safe workflow: $Code \rightarrow Plan \text{ (Review changes)} \rightarrow Apply$

**AWS CDK (Cloud Development Kit):**
- Allows defining infrastructure using programming languages (Python, TypeScript...)
- **Constructs:** From L1 (Detailed configuration) to L3 (Complex architecture patterns)
- **Drift Detection:** Important feature to detect discrepancies between Code and Reality (due to someone manually editing on Console)

#### 3. Containerization Strategy

Choosing a Container platform depends on scale and needs:

- **Amazon ECS:** Simple, deeply integrated with AWS, suitable for teams wanting quick operations
- **Amazon EKS:** Based on standard Kubernetes, large ecosystem, suitable for Enterprise or complex/Hybrid systems
- **AWS App Runner:** "Zero-ops" solution for Web App/API, automatically from Source/Image to HTTPS URL without server configuration

**Compute Options:**
- **EC2 Launch Type:** Highest control but costly operations (patching, scaling)
- **AWS Fargate (Serverless):** AWS handles infrastructure, users only need to define CPU/RAM for Tasks

#### 4. Observability - Monitoring & Optimization

Closing the development lifecycle with deep observation capability:

- **Amazon CloudWatch:** "Eyes and Ears" of the system (Metrics, Logs, Alarms)
- **AWS X-Ray:** Solves the "finding a needle in a haystack" problem in Microservices through Distributed Tracing (tracking requests through multiple services to find bottlenecks)

### III. EVALUATION & LESSONS LEARNED

Participating in this workshop series significantly changed my awareness and skills:

#### 1. Shift from "Ops" to "Platform Engineering"

I realized that the role of modern DevOps is not to chase after Developers to manually deploy code. DevOps is the architect of the "Highway" (Pipeline & Platform). A good Platform allows Developers to Self-service creating environments and deploying code quickly while staying within safe corridors (Governance) that the DevOps team establishes.

#### 2. Operational Discipline

Lessons on Artifact Management and Drift Detection are golden rules. In Enterprise environments, consistency is vital. Building differently across environments or manual changes to systems managed by code must be strictly prohibited.

#### 3. Smart Tool Selection Strategy

There is no "best" tool, only the "most appropriate" tool:

- Need absolute stability and deepest support for new AWS services $\rightarrow$ Choose CloudFormation
- Enterprise using Multi-cloud or Hybrid-cloud $\rightarrow$ Terraform is optimal
- Developer team strong in programming, needs to build complex architecture quickly and reuse code $\rightarrow$ AWS CDK
- Simple Web App $\rightarrow$ Use App Runner instead of spending resources operating Kubernetes cluster

### IV. CONCLUSION

Series "DevOps & IaC Mastery" provided a complete roadmap for the Cloud journey:

- **Mindset:** Shift from manual work to automation and measurement by metrics
- **Infrastructure:** Master IaC for scalable, reproducible systems and drift control
- **Operations:** Combine flexible Containerization and deep Observability to ensure stable, high-performance systems

This is a solid knowledge foundation for me to confidently build and operate large-scale software systems on AWS.

#### Some images from the event
* Add your images here

> Overall, the workshop helped me gain a comprehensive view of modern DevOps, from mindset, IaC tools, containerization strategy to observability, creating a solid foundation for building and operating Cloud-native systems.
