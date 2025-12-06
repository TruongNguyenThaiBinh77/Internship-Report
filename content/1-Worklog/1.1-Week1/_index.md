---
title: "Week 1 Worklog"
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1: Identity Management and Network Architecture (08/09 – 12/09)

**Objective:** Set up enterprise-standard AWS account and build secure Virtual Private Cloud (VPC).

### Tasks completed this week:

| Day | Date  | Task                                   | Activities                                                                                                                                                                     |
| --- | ----- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | 08/09 | **Account Setup & Cost Management**    | - Create AWS Account with Root User security (MFA enabled)<br>- Set up AWS Budgets for monthly cost and usage alerts<br>- Study AWS Support plans (Basic, Developer, Business) |
| 2   | 09/09 | **IAM - Part 1**                       | - Apply Principle of Least Privilege<br>- Create IAM Users and Groups (Admins, Developers, Auditors)<br>- Configure Account Password Policy (CIS Benchmark compliant)          |
| 3   | 10/09 | **IAM - Part 2**                       | - Create IAM Roles and Instance Profiles for EC2<br>- Write custom JSON policies for granular access control<br>- Practice EC2 accessing S3 via Instance Metadata Service      |
| 4   | 11/09 | **VPC Architecture - Theory & Design** | - Study VPC vs Default VPC concepts<br>- Plan IP address space (CIDR 10.0.0.0/16)<br>- Design Multi-AZ model with Public/Private Subnets                                       |
| 5   | 12/09 | **VPC Deployment**                     | - Create VPC, Subnets, Internet Gateway<br>- Configure Route Tables for Public/Private subnets<br>- Deploy NAT Gateway for Private subnet internet access                      |

### Week 1 Achievements:

- Understood foundational AWS service groups:

  - Compute (Amazon EC2)
  - Networking (Amazon VPC)
  - Identity & Access Management (IAM)
  - Billing & Cost Management (AWS Budgets)

- Successfully created and secured AWS Account with MFA on Root User

- Mastered IAM concepts:

  - Creating Users, Groups with Managed Policies
  - Writing custom JSON policies for granular access
  - IAM Roles for EC2 (Instance Profiles)

- Designed and deployed enterprise VPC:

  - Multi-AZ architecture for High Availability
  - Public Subnets for Load Balancers, Bastion Hosts
  - Private Subnets for Databases, Application Servers
  - NAT Gateway for secure outbound internet access

- Applied FinOps thinking with AWS Budgets from day one
