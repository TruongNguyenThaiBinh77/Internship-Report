---
title : "Testing the System"
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

## Testing the EV Rental AI Agent

In this section, you will test all three core features of the AI Agent to ensure everything works correctly.

### Prerequisites for Testing

Before testing, ensure:
- ✅ Backend server running on `http://localhost:8000`
- ✅ Frontend application running on `http://localhost:3000`
- ✅ PostgreSQL database is running and populated with test data
- ✅ AWS Bedrock Knowledge Base is synced and ready

### Test Scenario 1: Knowledge Base Search

The AI Agent should be able to answer questions about rental policies, pricing, and FAQs using the Knowledge Base.

**Test Queries:**

1. **Rental Policy:**
   ```
   User: "Chính sách thuê xe là gì?"
   Expected: Agent returns rental policy details from Knowledge Base
   ```

2. **Required Documents:**
   ```
   User: "Tôi cần giấy tờ gì để thuê xe?"
   Expected: Agent lists required documents (ID, license, deposit info)
   ```

3. **Pricing Information:**
   ```
   User: "Giá thuê xe VinFast VF8 là bao nhiêu?"
   Expected: Agent provides pricing details from Knowledge Base
   ```

4. **Booking Process:**
   ```
   User: "Làm thế nào để đặt xe?"
   Expected: Agent explains step-by-step booking process
   ```

**Verification:**
- ✅ Response includes citation from Knowledge Base
- ✅ Answer is relevant and accurate
- ✅ Markdown formatting displays correctly
- ✅ Response time is under 5 seconds

![Knowledge Base Search Test](/images/5-Workshop/5.6-Testing/image-12.png)

### Test Scenario 2: Vehicle Search

The AI Agent should search the PostgreSQL database for available vehicles based on location and date.

**Test Queries:**

1. **Search by Location:**
   ```
   User: "Tìm xe ở Hà Nội"
   Expected: Agent lists available vehicles in Hanoi
   ```

2. **Search by Model:**
   ```
   User: "Có xe VinFast VF8 nào available không?"
   Expected: Agent shows VF8 vehicles with availability status
   ```

3. **Search with Date Range:**
   ```
   User: "Tìm xe VF9 ở Hồ Chí Minh từ ngày 20/12 đến 25/12"
   Expected: Agent searches vehicles available in that date range
   ```

4. **Search with Price Range:**
   ```
   User: "Xe nào dưới 1 triệu đồng/ngày?"
   Expected: Agent filters vehicles by price
   ```

**Verification:**
- ✅ Agent correctly extracts search parameters (location, model, dates)
- ✅ Results include vehicle details (model, price, location, availability)
- ✅ Data is fetched from PostgreSQL database
- ✅ Results are formatted in a readable table or list

**Expected Response Format:**
```markdown
## 🚗 Available Vehicles

| Model | Location | Price/Day | Status |
|-------|----------|-----------|--------|
| VinFast VF8 | Hà Nội | 800,000đ | Available |
| VinFast VF9 | Hà Nội | 1,200,000đ | Available |
```

### Test Scenario 3: Charging Station Finder

The AI Agent should find nearby charging stations with real-time availability.

**Test Queries:**

1. **Search by District:**
   ```
   User: "Trạm sạc gần Quận Hoàn Kiếm"
   Expected: Agent lists charging stations in Hoan Kiem district
   ```

2. **Search by Address:**
   ```
   User: "Tìm trạm sạc ở Quận 1, TP.HCM"
   Expected: Agent finds stations in District 1, HCMC
   ```

3. **Check Station Availability:**
   ```
   User: "Trạm sạc nào còn trống?"
   Expected: Agent shows stations with available charging ports
   ```

4. **Filter by Connector Type:**
   ```
   User: "Trạm sạc có CCS2 connector"
   Expected: Agent filters stations with CCS2 connectors
   ```

**Verification:**
- ✅ Agent correctly identifies location from query
- ✅ Results include station name, address, and availability
- ✅ Connector types are listed
- ✅ Real-time availability status is shown

**Expected Response Format:**
```markdown
## ⚡ Charging Stations Near You

### VinFast Station - Hoàn Kiếm
📍 Address: 123 Trần Hưng Đạo, Hoàn Kiếm, Hà Nội
🔌 Connectors: CCS2 (2 available), CHAdeMO (1 available)
⏰ Hours: 24/7
✅ Status: Available
```

### Test Scenario 4: Multi-Turn Conversations

Test the agent's ability to maintain context across multiple turns.

**Test Conversation:**

```
User: "Tôi muốn thuê xe VF8"
Agent: [Provides VF8 information]

User: "Giá bao nhiêu?"
Agent: [Should understand context refers to VF8 pricing]

User: "Trạm sạc gần đó ở đâu?"
Agent: [Should find charging stations near VF8 location]
```

**Verification:**
- ✅ Agent maintains conversation context
- ✅ Pronouns and references are resolved correctly
- ✅ Session ID persists across messages

### Test Scenario 5: Error Handling

Test how the agent handles invalid or unclear queries.

**Test Cases:**

1. **Ambiguous Query:**
   ```
   User: "Xe"
   Expected: Agent asks for clarification
   ```

2. **Unavailable Vehicle:**
   ```
   User: "Tìm xe Tesla"
   Expected: Agent explains Tesla is not available, suggests alternatives
   ```

3. **Invalid Date:**
   ```
   User: "Thuê xe từ ngày 32/13"
   Expected: Agent detects invalid date and asks for correction
   ```

4. **Out of Scope:**
   ```
   User: "What's the weather today?"
   Expected: Agent politely explains it can only help with EV rentals
   ```

**Verification:**
- ✅ Agent handles errors gracefully
- ✅ Provides helpful error messages
- ✅ Suggests alternatives when possible

### Performance Testing

Check system performance under normal usage:

**Metrics to Monitor:**

1. **Response Time:**
   - Knowledge Base queries: < 3 seconds
   - Vehicle search: < 2 seconds
   - Charging station search: < 2 seconds

2. **API Health:**
   ```bash
   curl http://localhost:8000/health
   ```
   Expected: `200 OK` with health status

3. **Backend Logs:**
   Check for errors in FastAPI console output

4. **Frontend Console:**
   Open browser DevTools → Console
   - No JavaScript errors
   - API calls succeed (Network tab)

### Integration Testing Checklist

Run through this comprehensive checklist:

- ✅ **Knowledge Base Integration:**
  - Agent can retrieve policy information
  - Citations are included in responses
  - Bedrock API calls succeed

- ✅ **Database Integration:**
  - Vehicle search queries PostgreSQL
  - Results are accurate and up-to-date
  - Database connection is stable

- ✅ **Backend API:**
  - `/api/chat` endpoint works
  - `/health` endpoint responds
  - Session management functions correctly

- ✅ **Frontend UI:**
  - Messages display correctly
  - User input is captured
  - Loading states work
  - Markdown renders properly
  - Auto-scroll functions

- ✅ **Error Handling:**
  - Network errors are caught
  - Invalid inputs handled gracefully
  - User receives helpful feedback

### Testing with Postman (Optional)

Test backend API directly:

**1. Health Check:**
```http
GET http://localhost:8000/health
```

**2. Chat Request:**
```http
POST http://localhost:8000/api/chat
Content-Type: application/json

{
  "session_id": "test-session-123",
  "message": "Chính sách thuê xe là gì?"
}
```

**Expected Response:**
```json
{
  "response": "## 📋 Chính sách thuê xe VinFast\n\n...",
  "data": null,
  "session_id": "test-session-123"
}
```

### Troubleshooting Test Failures

**Issue: Knowledge Base returns empty results**
- Check Knowledge Base is synced in AWS Console
- Verify KNOWLEDGE_BASE_ID in `.env`
- Test KB directly in Bedrock console

**Issue: Vehicle search returns no results**
- Check PostgreSQL database has test data
- Verify DATABASE_URL connection string
- Run SQL query directly: `SELECT * FROM vehicles;`

**Issue: Charging stations not found**
- Verify backend API `/stations` endpoint works
- Check station data in database
- Test API call: `curl http://localhost:8080/stations`

**Issue: Frontend not connecting to backend**
- Check REACT_APP_API_URL in frontend `.env`
- Verify backend CORS allows `http://localhost:3000`
- Check browser console for network errors

### Test Report Template

Document your test results:

```markdown
## Test Report - EV Rental AI Agent

**Date:** 2024-12-20
**Tester:** Your Name

### Test Results Summary
- Total Tests: 15
- Passed: 14
- Failed: 1
- Success Rate: 93%

### Detailed Results

#### Knowledge Base Search
- [x] Rental policy query - PASS
- [x] Required documents - PASS
- [x] Pricing information - PASS
- [ ] Booking process - FAIL (slow response)

#### Vehicle Search
- [x] Search by location - PASS
- [x] Search by model - PASS
- [x] Date range search - PASS

#### Charging Station Finder
- [x] District search - PASS
- [x] Availability check - PASS

### Issues Found
1. Booking process query takes 7 seconds (> 5s threshold)
   - Root cause: Knowledge Base sync incomplete
   - Fix: Re-sync data source

### Recommendations
- Monitor response times during peak usage
- Add caching for frequently asked questions
- Implement rate limiting
```

---

**Success!** 🎉 Your EV Rental AI Agent is now fully tested and operational.

**Next:** Proceed to [Cleanup](../5.7-Cleanup/) to remove resources and avoid charges.
