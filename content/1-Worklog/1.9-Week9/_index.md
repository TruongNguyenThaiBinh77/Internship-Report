---
title: "Week 9 Worklog"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9: AWS Containers & Voltgo Login/User Modules (03/11 - 07/11)

**Dual Objective:** Master Docker and container orchestration platforms on AWS, while building Authentication pages for Voltgo.

---

## PART A: AWS - Container Technology

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 03/11 | **Docker Fundamentals** | - Write optimized Dockerfile (Multi-stage build)<br>- Create ECR Repository<br>- Push private image to ECR |
| 2 | 04/11 | **Amazon ECS & Fargate** | - Create Task Definition with CPU/RAM specs<br>- Deploy ECS Service with Fargate<br>- Integrate with Application Load Balancer |
| 3 | 05/11 | **Amazon EKS Setup** | - Create EKS cluster with eksctl<br>- Configure Managed Node Groups<br>- AWS handles patching and upgrades |
| 4 | 06/11 | **Deploy on EKS** | - Write K8s YAML manifests (Deployment, Service, Ingress)<br>- Install AWS Load Balancer Controller<br>- Auto-create ALB from Ingress |
| 5 | 07/11 | **CI/CD for Containers** | - Build CI/CD Pipeline for ECS/EKS<br>- CodeCommit -> CodeBuild -> CodeDeploy<br>- Blue/Green Deployment strategy |

---

## PART B: Voltgo - Login & User Modules

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 03/11 | **Login Page** | - Build Login UI with React Hook Form + Yup validation<br>- Remember Me with localStorage<br>- Forgot Password flow with OTP |
| 2 | 04/11 | **Register Page** | - Registration form: name, email, phone, password<br>- User type selection: Personal/Business<br>- Terms & Conditions checkbox |
| 3 | 05/11 | **Authentication API** | - Connect to POST /api/auth/login, /register<br>- JWT token management with auto-refresh<br>- Protected Routes for Booking, Profile |
| 4 | 06/11 | **User Profile Page** | - Display avatar, name, email, phone, address<br>- Inline editing form<br>- Driver License upload (required for rental) |
| 5 | 07/11 | **Complete User Module** | - Booking history in User page<br>- Favorite vehicles feature<br>- Payment methods management<br>- Notification settings |

### Week 9 Achievements:

* **AWS Containers:**
  * Deployed containers on ECS Fargate (serverless)
  * Set up EKS cluster with managed node groups
  * Built CI/CD pipeline for container applications

* **Voltgo Login & User:**
  * Complete Login/Register pages with validation
  * JWT authentication integrated
  * User profile with avatar, driver license upload
  * Booking history and payment methods in User page
