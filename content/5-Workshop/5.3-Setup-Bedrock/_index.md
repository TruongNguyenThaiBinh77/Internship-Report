---
title : "Setup AWS Bedrock"
weight : 3 
chapter : false
pre : " <b> 5.3. </b> "
---

## Setting up AWS Bedrock & Knowledge Base

In this section, you will configure AWS Bedrock to use Claude 3.5 Sonnet and create a Knowledge Base for document retrieval.

### Step 1: Enable Model Access

**IMPORTANT:** You must enable model access before using Bedrock, otherwise you'll get `ValidationException` errors.

1. Go to **AWS Console → Services → Bedrock**
2. In the left sidebar, click **Model access** (under Foundation models)
3. Click **Manage model access** button (orange)
4. Find and select these models:
   - ✅ **Anthropic - Claude 3.5 Sonnet v2** (`anthropic.claude-3-5-sonnet-20241022-v2:0`)
   - ✅ **Amazon - Titan Embeddings G1 - Text** (for Knowledge Base)
5. Click **Request model access** (bottom right)
6. Wait for approval:
   - **Instant access models**: Available immediately (green ✅)
   - **Other models**: Wait 5-30 minutes (status changes from "In progress" → "Access granted")

![Enable Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-4.png)
![Enable Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-5.png)
![Enable Model Access](/images/5-Workshop/5.3-Setup-Bedrock/image-6.png)

**Verify models are enabled:**
```bash
# Using AWS CLI
aws bedrock list-foundation-models --region us-west-2

# Or check in Console:
# Bedrock → Model access → Status must be "Access granted"
```

### Step 2: Create S3 Bucket for Knowledge Base

Knowledge Base requires an S3 bucket to store documents.

1. Go to **S3 → Create bucket**
2. Bucket name: `ev-rental-knowledge-docs` (must be globally unique)
3. Region: Same as your Bedrock region (e.g., `us-west-2`)
4. **Block all public access**: ✅ Enabled (recommended)
5. Click **Create bucket**

![Create S3 Bucket](/images/5-Workshop/5.3-Setup-s3/image-7.png)
![Create S3 Bucket](/images/5-Workshop/5.3-Setup-s3/image-8.png)

### Step 3: Upload Documents to S3

Upload your rental policy documents (PDF, TXT, DOCX):

**Sample documents to upload:**
- `rental-policy.pdf` - Rental policies and terms
- `pricing.pdf` - Vehicle pricing information
- `faq.txt` - Frequently asked questions
- `booking-process.pdf` - How to book a vehicle

**Upload via Console:**
1. Go to your S3 bucket: `ev-rental-knowledge-docs`
2. Click **Upload** → **Add files**
3. Select your documents
4. Click **Upload**

**Upload via AWS CLI:**
```bash
aws s3 cp rental-policy.pdf s3://ev-rental-knowledge-docs/
aws s3 cp pricing.pdf s3://ev-rental-knowledge-docs/
aws s3 cp faq.txt s3://ev-rental-knowledge-docs/
aws s3 cp booking-process.pdf s3://ev-rental-knowledge-docs/
```

### Step 4: Create Knowledge Base

1. Go to **Bedrock → Knowledge Bases → Create**
2. **Knowledge base name**: `ev-rental-knowledge-base`
3. **Description**: "VinFast EV rental policies and FAQs"
4. Click **Next**

![Create Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-9.png)
![Create Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-10.png)

**Data source configuration:**
1. **Data source name**: `rental-docs`
2. **S3 URI**: `s3://ev-rental-knowledge-docs/`
3. Click **Next**
![Create Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-11.png)

**Embeddings model:**
1. Select: **Titan Embeddings G1 - Text** (`amazon.titan-embed-text-v1`)
2. **Vector database**: Choose **Bedrock managed (OpenSearch Serverless)** (easiest option)
3. Click **Next**
![Create Knowledge Base](/images/5-Workshop/5.4-Setup-knowledgebase/image-12.png)



**Review and create:**
1. Review all settings
2. Click **Create knowledge base**
3. Wait for creation to complete (2-3 minutes)

### Step 5: Sync Data Source

After Knowledge Base is created, you need to sync the data:

1. In your Knowledge Base, go to **Data sources** tab
2. Select your data source: `rental-docs`
3. Click **Sync** button
4. Wait for sync to complete (check status: "Syncing" → "Ready")
5. This process indexes all documents and creates vector embeddings


**Sync status:**
- 🔄 **Syncing**: In progress
- ✅ **Ready**: Completed successfully
- ❌ **Failed**: Check S3 permissions or document formats

### Step 6: Get Knowledge Base ID

You'll need this ID for your backend application:

1. In your Knowledge Base page
2. Copy the **Knowledge Base ID** (format: `89CI1JSSE4` or similar)
3. Save it in your notes - you'll use it in the next step

**Example Knowledge Base ID:**
```
Knowledge Base ID: 89CI1JSSE4
Knowledge Base ARN: arn:aws:bedrock:us-west-2:123456789:knowledge-base/89CI1JSSE4
```

### Step 7: Test Knowledge Base (Optional)

Test your Knowledge Base directly in the console:

1. Go to your Knowledge Base
2. Click **Test** tab
3. Enter a question: "What is the rental policy?"
4. Click **Run**
5. Verify it returns relevant information from your documents

### Verification Checklist

Before moving to the next step, ensure:

- ✅ Claude 3.5 Sonnet v2 model access is **granted**
- ✅ Titan Embeddings model access is **granted**
- ✅ S3 bucket created with documents uploaded
- ✅ Knowledge Base created and data synced successfully
- ✅ Knowledge Base ID saved
- ✅ Test query returns relevant results

### Troubleshooting

**Issue: "ValidationException: Model not enabled"**
- Solution: Go to Bedrock → Model access and enable the model

**Issue: "Sync failed"**
- Check S3 bucket permissions
- Verify document formats (PDF, TXT, DOCX supported)
- Check CloudWatch Logs for detailed errors

**Issue: "No results from Knowledge Base"**
- Ensure documents are uploaded to S3
- Run sync again
- Wait a few minutes after sync completes
- Try different query phrasing

---

**Next:** Proceed to [Deploy Backend API](../5.4-Deploy-Backend/) to build the FastAPI server.
