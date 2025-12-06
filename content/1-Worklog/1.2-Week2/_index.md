---
title: "Week 2 Worklog"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2: Basic Computing and Storage (15/09 – 19/09)

**Objective:** Deploy virtual servers (EC2), understand storage types (EBS, S3) and simplified compute models (Lightsail).

### Tasks completed this week:

| Day | Date  | Task                                | Activities                                                                                                                                                                                             |
| --- | ----- | ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | 15/09 | **Amazon EC2 - Launch & Connect**   | - Analyze instance types: T3 (Burstable), C5 (Compute), R5 (Memory)<br>- Launch Amazon Linux 2023 instance<br>- SSH connection with Key Pairs (.pem/.ppk)                                              |
| 2   | 16/09 | **EBS Storage & Windows Workloads** | - Create and mount gp3 EBS volume to Linux instance<br>- Deploy Windows Server 2022, connect via RDP<br>- Create EBS Snapshots for backup                                                              |
| 3   | 17/09 | **Cloud9 Development Environment**  | - Set up browser-based IDE with AWS CLI, SAM, Docker pre-installed<br>- Remote access without opening SSH port<br>- Experience code editing and terminal directly from browser                         |
| 4   | 18/09 | **Amazon S3 Basics**                | - Create S3 Bucket and upload media files<br>- Configure Static Website Hosting<br>- Write Bucket Policy JSON for public GetObject access                                                              |
| 5   | 19/09 | **S3 Advanced & Security**          | - Analyze Storage Classes: Standard, Intelligent-Tiering, Glacier<br>- Set up Lifecycle Policy to move old objects to Glacier<br>- Enable Block Public Access, Versioning, Default Encryption (SSE-S3) |

### Week 2 Achievements:

- **EC2 Mastery:**

  - Understand instance type families and use cases
  - Successfully launched and connected to both Linux and Windows instances
  - Created EBS volumes and snapshots for data persistence

- **Cloud Development:**

  - Set up Cloud9 IDE eliminating local environment issues
  - Experienced managed access without public SSH ports

- **Object Storage:**

  - Deployed S3 static website with proper access policies
  - Implemented cost optimization with Lifecycle Policies
  - Applied security best practices: Block Public Access, Versioning, Encryption

- **Key Concepts:**
  - EBS is persistent storage independent of EC2 lifecycle
  - S3 provides unlimited scalable object storage
  - Incremental backup mechanism with Snapshots
