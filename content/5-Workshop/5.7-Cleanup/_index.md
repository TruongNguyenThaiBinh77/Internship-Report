---
title : "Cleanup Resources"
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## Cleaning Up Resources

After completing the workshop, follow these steps to clean up all resources and avoid unnecessary AWS charges.

### Why Cleanup is Important

- **Cost Savings:** AWS charges for active resources like Bedrock Knowledge Bases, S3 storage, and running services
- **Security:** Remove unused IAM credentials to maintain security best practices
- **Organization:** Keep your AWS account clean and organized

---

## Step 1: Delete AWS Bedrock Knowledge Base

### 1.1 Delete Knowledge Base

1. Open the **AWS Bedrock Console**
2. Navigate to **Knowledge Bases** in the left sidebar
3. Select your Knowledge Base: `ev-rental-knowledge-base`
4. Click **Delete**
5. Confirm deletion by typing the Knowledge Base name
6. Click **Delete** to confirm

⚠️ **Note:** This will also delete the associated data source connections.

### 1.2 Delete S3 Bucket and Documents

1. Open the **S3 Console**
2. Find your bucket: `ev-rental-knowledge-docs`
3. Select the bucket
4. Click **Empty** to delete all objects
5. Confirm by typing "permanently delete"
6. After emptying, click **Delete** on the bucket
7. Confirm by typing the bucket name

**Or use AWS CLI:**
```bash
# Delete all objects in bucket
aws s3 rm s3://ev-rental-knowledge-docs --recursive

# Delete the bucket
aws s3 rb s3://ev-rental-knowledge-docs
```

---

## Step 2: Delete IAM User and Access Keys

### 2.1 Delete Access Keys

1. Open the **IAM Console**
2. Navigate to **Users**
3. Select your user (e.g., `bedrock-agent-user`)
4. Click on the **Security credentials** tab
5. Under **Access keys**, find your access key
6. Click **Delete** next to the access key
7. Confirm deletion

### 2.2 Delete IAM User (Optional)

If you created a dedicated IAM user for this workshop:

1. In the IAM Console, select the user
2. Click **Delete user**
3. Confirm by checking the box
4. Click **Delete**

**Or use AWS CLI:**
```bash
# List access keys
aws iam list-access-keys --user-name bedrock-agent-user

# Delete access key (replace with your key ID)
aws iam delete-access-key --user-name bedrock-agent-user --access-key-id AKIA5GPEMGJZK6E7PMEB

# Delete user
aws iam delete-user --user-name bedrock-agent-user
```

---

## Step 3: Stop Local Services

### 3.1 Stop FastAPI Backend

In the terminal where FastAPI is running:

1. Press `Ctrl + C` to stop the server
2. Deactivate virtual environment:
   ```bash
   deactivate
   ```

3. Optionally delete the project folder:
   ```bash
   # On macOS/Linux
   rm -rf ev-rental-backend
   
   # On Windows
   rmdir /s ev-rental-backend
   ```

### 3.2 Stop React Frontend

In the terminal where React is running:

1. Press `Ctrl + C` to stop the development server

2. Optionally delete the project folder:
   ```bash
   # On macOS/Linux
   rm -rf ev-rental-frontend
   
   # On Windows
   rmdir /s ev-rental-frontend
   ```

### 3.3 Stop PostgreSQL Database

If you installed PostgreSQL locally for this workshop:

**On macOS:**
```bash
# Stop PostgreSQL service
brew services stop postgresql@14
```

**On Linux:**
```bash
sudo systemctl stop postgresql
```

**On Windows:**
```bash
# Open Services (services.msc)
# Find "PostgreSQL" service
# Right-click → Stop
```

### 3.4 Delete Database (Optional)

If you want to completely remove the database:

```bash
# Connect to PostgreSQL
psql -U postgres

# Drop database
DROP DATABASE ev_rental_db;

# Exit
\q
```

---

## Step 4: Remove Environment Files

Delete sensitive `.env` files that contain credentials:

**Backend:**
```bash
cd ev-rental-backend
rm .env
```

**Frontend:**
```bash
cd ev-rental-frontend
rm .env
```

⚠️ **Security Note:** Never commit `.env` files to Git. Always add them to `.gitignore`.

---

## Step 5: Verify Cleanup

### 5.1 Check AWS Resources

Verify all resources are deleted:

1. **Bedrock Console:**
   - No Knowledge Bases listed
   - No model invocations active

2. **S3 Console:**
   - Bucket `ev-rental-knowledge-docs` is deleted

3. **IAM Console:**
   - Access keys are deleted
   - IAM user removed (if you chose to delete it)

### 5.2 Check AWS Costs

1. Open the **AWS Billing Console**
2. Check **Bills** for the current month
3. Verify charges:
   - Bedrock charges should stop after Knowledge Base deletion
   - S3 storage charges should stop after bucket deletion
   - No ongoing compute charges

**Or use AWS CLI:**
```bash
aws ce get-cost-and-usage \
  --time-period Start=2024-12-01,End=2024-12-31 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=SERVICE
```

---

## Cost Breakdown

Here's what you may have been charged during the workshop:

| Service | Estimated Cost | Notes |
|---------|---------------|-------|
| **AWS Bedrock - Claude 3.5 Sonnet** | ~$0.50 - $2.00 | Depends on number of queries |
| **AWS Bedrock - Knowledge Base** | ~$0.10 - $0.50 | Vector storage and retrieval |
| **S3 Storage** | ~$0.02 | Minimal for small documents |
| **Data Transfer** | ~$0.05 | Usually within free tier |
| **Total** | ~$0.67 - $2.57 | Approximate for workshop |

⚠️ **Note:** Most costs come from Bedrock API calls. The longer you test, the higher the cost.

---

## Cleanup Checklist

Before you finish, verify all items are complete:

### AWS Resources
- ✅ Bedrock Knowledge Base deleted
- ✅ S3 bucket emptied and deleted
- ✅ IAM Access Keys deleted
- ✅ IAM User deleted (optional)

### Local Resources
- ✅ FastAPI backend stopped
- ✅ React frontend stopped
- ✅ PostgreSQL database stopped
- ✅ PostgreSQL database dropped (optional)

### Sensitive Files
- ✅ Backend `.env` file deleted
- ✅ Frontend `.env` file deleted
- ✅ No AWS credentials in project files

### Verification
- ✅ AWS Console shows no active resources
- ✅ Billing dashboard shows stopped charges
- ✅ Local services not running

---

## Troubleshooting Cleanup Issues

**Issue: Cannot delete S3 bucket - "Bucket not empty"**
- Solution: Empty all objects first using the S3 Console or CLI
- Command: `aws s3 rm s3://bucket-name --recursive`

**Issue: Cannot delete Knowledge Base - "In use"**
- Solution: Wait a few minutes for any pending operations to complete
- Check if any API calls are still referencing it

**Issue: IAM User deletion fails - "User has attached policies"**
- Solution: Detach all policies first
- Go to IAM → Users → Select user → Permissions → Detach policies

**Issue: PostgreSQL won't stop**
- Solution: Force kill the process
- On macOS/Linux: `sudo killall postgres`
- On Windows: Use Task Manager to end PostgreSQL processes

---

## Optional: Keep Learning

If you want to continue experimenting:

### Keep These Resources:
- ✅ IAM User (with minimal permissions)
- ✅ Bedrock model access (no charge when not in use)

### What You Can Do Next:
- Add more documents to Knowledge Base
- Implement additional agent tools
- Deploy to AWS Lambda for serverless operation
- Add authentication and user management
- Integrate with real vehicle booking systems

---

## Conclusion

🎉 **Congratulations!** You have successfully:

1. ✅ Built an AI Agent using AWS Bedrock and Claude 3.5 Sonnet
2. ✅ Integrated Knowledge Bases for intelligent document retrieval
3. ✅ Created a FastAPI backend with Strands Agent SDK
4. ✅ Developed a React frontend for user interaction
5. ✅ Tested all features end-to-end
6. ✅ Cleaned up resources to avoid charges

### Key Takeaways:

- **AI Agents** can autonomously select tools and make decisions
- **AWS Bedrock** simplifies access to foundation models like Claude
- **Knowledge Bases** enable semantic search over documents
- **Strands SDK** provides a framework for building agent workflows
- **FastAPI + React** create a modern full-stack AI application

### Next Steps:

- Explore other Bedrock models (Llama 3, Mistral, etc.)
- Learn about RAG (Retrieval Augmented Generation)
- Build more complex agent workflows
- Deploy to production using AWS services

---


