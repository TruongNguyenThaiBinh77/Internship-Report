---
title: "Week 10 Worklog"
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10: AWS Serverless & Voltgo Vehicle/Station Modules (10/11 - 14/11)

**Dual Objective:** Build serverless applications on AWS and develop Vehicle/Station features for Voltgo.

---

## PART A: AWS - Serverless Architecture

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 10/11 | **Serverless Trio** | - Write AWS Lambda for CRUD operations<br>- Integrate with DynamoDB<br>- Build REST API with API Gateway |
| 2 | 11/11 | **Serverless Auth & Security** | - Deploy Cognito Authorizer on API Gateway<br>- Configure Custom Domains and SSL |
| 3 | 12/11 | **Event-Driven Architecture** | - Process orders with SQS and SNS<br>- Configure S3 triggers for thumbnail generation |
| 4 | 13/11 | **Step Functions** | - Build workflow orchestration<br>- Create order approval process: Check inventory -> Charge -> Send email |
| 5 | 14/11 | **X-Ray Tracing** | - Enable distributed tracing<br>- Observe service map: API Gateway -> Lambda -> DynamoDB |

---

## PART B: Voltgo - Vehicle & Station Modules

| Day | Date | Task | Activities |
| --- | ---- | ---- | ---------- |
| 1 | 10/11 | **Vehicle List Page** | - Build vehicle list with grid/list toggle<br>- VehicleCard: image, name, type, price, battery, status<br>- Filter by type, price, range |
| 2 | 11/11 | **Vehicle Detail Page** | - Image gallery, specifications display<br>- Pricing table (hourly, daily, weekly)<br>- Availability calendar, reviews section |
| 3 | 12/11 | **Station List Page** | - Station list with StationCard component<br>- Google Maps/Mapbox integration<br>- Nearby stations with Geolocation API |
| 4 | 13/11 | **Station Detail Page** | - Full station info: address, hours, amenities<br>- Available vehicles at station<br>- Charging slots status, directions |
| 5 | 14/11 | **Map View & Real-time** | - Full-screen map with all stations/vehicles<br>- Custom markers (station=green, vehicle=yellow)<br>- Marker clustering, real-time updates |

### Week 10 Achievements:

* **AWS Serverless:**
  * Built complete serverless API with Lambda, API Gateway, DynamoDB
  * Implemented event-driven architecture with SQS/SNS
  * Orchestrated workflows with Step Functions
  * Enabled distributed tracing with X-Ray

* **Voltgo Vehicle & Station:**
  * Complete Vehicle List and Detail pages
  * Station pages with map integration
  * Real-time vehicle/station status updates
  * Geolocation for nearby stations
