---
title: "Week 4 Worklog"
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Week 4: Scalability, Monitoring and Content Distribution (29/09 – 03/10)

**Objective:** Automate system scalability, set up comprehensive monitoring, and optimize global content distribution.

### Tasks completed this week:

| Day | Date  | Task                             | Activities                                                                                                                                                                         |
| --- | ----- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | 29/09 | **EC2 Auto Scaling**             | - Create Launch Templates with AMI, Instance Type, Security Group<br>- Set up Auto Scaling Group (Min=2, Max=4, Desired=2)<br>- Configure Target Tracking Scaling Policy (CPU 50%) |
| 2   | 30/09 | **Amazon CloudWatch Monitoring** | - Monitor standard metrics (CPU, Disk I/O, Network)<br>- Install CloudWatch Agent for Memory metrics<br>- Create Alarms with SNS notifications                                     |
| 3   | 01/10 | **Advanced Monitoring & Logs**   | - Configure CloudWatch Agent to push application logs<br>- Create CloudWatch Dashboard for system health overview<br>- Explore Grafana integration                                 |
| 4   | 02/10 | **Amazon Route 53 DNS**          | - Create Hosted Zone for domain management<br>- Practice routing policies: Simple, Failover, Latency-based<br>- Configure Health Checks for automatic failover                     |
| 5   | 03/10 | **Amazon CloudFront CDN**        | - Deploy CloudFront distribution for S3 static content<br>- Configure OAC (Origin Access Control)<br>- Customize TTL caching policies                                              |

### Week 4 Achievements:

- **Auto Scaling:**

  - Deployed Auto Scaling Group with Launch Templates
  - Tested scale out/in with stress tool
  - Integrated with Application Load Balancer

- **Monitoring:**

  - Built comprehensive CloudWatch Dashboard
  - Configured alarms for CPU, Memory, Disk metrics
  - Set up SNS notifications for alerts

- **DNS & CDN:**

  - Configured Route 53 with multiple routing policies
  - Deployed CloudFront for global content distribution
  - Implemented OAC for secure S3 access through CDN

- **Key Concepts:**
  - Horizontal scaling with Auto Scaling Groups
  - Proactive monitoring vs reactive troubleshooting
  - Edge locations for low-latency content delivery
