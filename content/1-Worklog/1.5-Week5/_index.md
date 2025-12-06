---
title: "Week 5 Worklog"
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Week 5: Operations and Infrastructure as Code (06/10 - 10/10)

**Objective:** Eliminate manual operations, manage server fleets at scale, and codify infrastructure.

### Tasks completed this week:

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 06/10 | **AWS Systems Manager** | - Configure SSM Agent with IAM Role<br>- Run Command on multiple instances<br>- Collect software inventory for auditing |
| 2 | 07/10 | **Session Manager Secure Access** | - Close port 22 (SSH) on Security Groups<br>- Access via HTTPS Session Manager<br>- Log all sessions to S3/CloudWatch |
| 3 | 08/10 | **CloudFormation IaC** | - Write YAML templates for VPC and EC2<br>- Practice Stack creation, update, delete<br>- Use Change Sets and Drift Detection |
| 4 | 09/10 | **AWS CDK Basics** | - Use TypeScript/Python for infrastructure<br>- Learn Construct levels (L1, L2, L3)<br>- Create VPC with single line of code |
| 5 | 10/10 | **AWS CDK Advanced & Workshop** | - Build reusable custom Constructs<br>- Handle circular dependencies<br>- Manage environment variables with Context |

### Week 5 Achievements:

* **Systems Management:**
  * Eliminated SSH key management with Session Manager
  * Ran commands on fleet without individual access
  * Collected inventory for compliance auditing

* **Infrastructure as Code:**
  * Wrote CloudFormation templates in YAML
  * Understood Stack lifecycle and state management
  * Detected configuration drift

* **AWS CDK:**
  * Used programming language for infrastructure
  * Built reusable Constructs for organization
  * Completed IaC Workshop challenges

* **Key Concepts:**
  * IaC eliminates manual configuration errors
  * Session Manager is the gold standard for server access
  * CDK provides higher abstraction than CloudFormation
