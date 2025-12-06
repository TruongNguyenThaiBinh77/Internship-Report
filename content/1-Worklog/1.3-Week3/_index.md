---
title: "Week 3 Worklog"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3: Databases and Managed Services (22/09 – 26/09)

**Objective:** Transition from self-managed databases on EC2 to Managed Database services (RDS, DynamoDB) to reduce operational overhead.

### Tasks completed this week:

| Day | Date  | Task                            | Activities                                                                                                                                                         |
| --- | ----- | ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1   | 22/09 | **Amazon RDS Deployment**       | - Deploy RDS with MySQL/PostgreSQL engine<br>- Enable Multi-AZ for high availability<br>- Analyze Synchronous Replication and automatic failover mechanism         |
| 2   | 23/09 | **RDS Connection & Operations** | - Configure Security Group allowing only App-Tier access<br>- Customize DB config via Parameter Groups<br>- Practice Automated Backups and Manual Snapshots        |
| 3   | 24/09 | **Amazon DynamoDB - Part 1**    | - Create DynamoDB table with Partition Key<br>- Understand SQL vs NoSQL schema differences<br>- Compare Provisioned vs On-Demand capacity modes                    |
| 4   | 25/09 | **DynamoDB Advanced - Part 2**  | - Practice API operations: PutItem, GetItem, Query, Scan<br>- Understand Query vs Scan efficiency<br>- Create Global Secondary Index (GSI) for alternative queries |
| 5   | 26/09 | **Amazon ElastiCache**          | - Deploy ElastiCache with Redis engine<br>- Implement Lazy Loading caching strategy<br>- Place cache cluster in Private Subnet for security                        |

### Week 3 Achievements:

- **Relational Database:**

  - Deployed RDS with Multi-AZ for high availability
  - Understood synchronous replication and automatic failover
  - Configured secure access through Security Groups

- **NoSQL Database:**

  - Designed DynamoDB tables with proper key schema
  - Understood differences between Query (efficient) vs Scan (expensive)
  - Implemented GSI for flexible query patterns

- **Caching Layer:**

  - Deployed ElastiCache Redis for application caching
  - Applied Lazy Loading pattern to reduce RDS load
  - Placed cache in Private Subnet for optimal latency

- **Key Concepts:**
  - Managed services reduce operational burden
  - Multi-AZ ensures business continuity
  - Proper database selection based on use case (SQL vs NoSQL)
