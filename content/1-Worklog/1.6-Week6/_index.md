---
title: "Week 6 Worklog"
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6: Multi-layer Security Architecture (13/10 - 17/10)

**Objective:** Build a digital fortress to protect data and applications from modern cyber threats.

### Tasks completed this week:

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 13/10 | **AWS WAF** | - Deploy WAF on ALB/CloudFront<br>- Configure rules against SQL Injection, XSS<br>- Create Rate-based rules for DDoS protection |
| 2 | 14/10 | **AWS KMS Encryption** | - Create Customer Managed Keys (CMK)<br>- Configure Key Policy for admin/user separation<br>- Enable encryption on EBS and S3 |
| 3 | 15/10 | **Secrets Manager** | - Store RDS passwords in Secrets Manager<br>- Configure automatic rotation with Lambda<br>- Update application to retrieve secrets via API |
| 4 | 16/10 | **GuardDuty Threat Detection** | - Enable intelligent threat detection<br>- Analyze CloudTrail, VPC Flow Logs, DNS Logs<br>- Configure EventBridge alerts for high-severity findings |
| 5 | 17/10 | **Amazon Cognito** | - Create User Pool for app authentication<br>- Configure Identity Pool for temporary AWS credentials<br>- Enable direct S3 upload from end users |

### Week 6 Achievements:

* **Application Security:**
  * Deployed WAF protecting against OWASP Top 10
  * Implemented rate limiting for DDoS mitigation

* **Data Encryption:**
  * Created and managed CMK with proper key policies
  * Encrypted data at rest across EBS, S3, RDS

* **Secrets Management:**
  * Eliminated hardcoded credentials in applications
  * Automated password rotation

* **Threat Detection:**
  * Enabled ML-based threat detection with GuardDuty
  * Set up automated alerting for security incidents

* **Identity Federation:**
  * Built user authentication with Cognito User Pools
  * Enabled federated access with Identity Pools
