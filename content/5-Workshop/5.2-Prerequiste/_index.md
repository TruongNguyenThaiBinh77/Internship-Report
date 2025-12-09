---
title : "Prerequisites"
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

## Prerequisites for EV Rental AI Agent Workshop

Before starting this workshop, ensure you have the following requirements ready:

### 1. AWS Account

You need an **AWS Account** with appropriate permissions to:
- Access AWS Bedrock service
- Create and manage IAM users
- Create S3 buckets (for Knowledge Base)
- Create Knowledge Bases

**Note:** Bedrock is available in specific regions. Recommended regions:
- `us-west-2` (Oregon)
- `us-east-1` (N. Virginia)  
- `ap-southeast-1` (Singapore)


### 2. IAM User with Bedrock Permissions

You need to create an IAM User with AWS Bedrock access for your application.

**Step 1: Create IAM User**
1. Go to **AWS Console → IAM → Users → Create User**

![AWS](/images/5-Workshop/5.2-Prerequiste/image.png)

![AWS](/images/5-Workshop/5.2-Prerequiste/image-1.png)

2. User name: `bedrock-agent-user`
3. ✅ Check: **Provide user access to the AWS Management Console** (optional)
4. ✅ Select: **I want to create an IAM user**
5. Click **Next**

**Step 2: Attach Permissions**
1. Select: **Attach policies directly**
2. Search and select these policies:
   - ✅ `AmazonBedrockFullAccess` - Full access to Bedrock models and Knowledge Bases
   - ✅ (Optional) `AmazonS3ReadOnlyAccess` - If using Knowledge Base with S3
3. Click **Next** → **Create User**

![AWS](/images/5-Workshop/5.2-Prerequiste/image-2.png)

**Step 3: Create Access Keys**
1. Click on the newly created user: `bedrock-agent-user`
2. Go to **Security credentials** tab
3. Scroll down to **Access keys** → Click **Create access key**
4. Select use case: **Application running outside AWS**
5. Click **Next** → **Create access key**
6. ⚠️ **IMPORTANT**: Copy and save:
   - `Access Key ID` (example: `AKIAIOSFODNN7EXAMPLE`)
   - `Secret Access Key` (shown only once, example: `wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY`)
7. Click **Done**

![AWS](/images/5-Workshop/5.2-Prerequiste/image-3.png)

⚠️ **Security Note:**
```bash
# Save to .env file (DO NOT commit to Git)
AWS_ACCESS_KEY_ID=YOUR_ACCESS_KEY_ID_HERE
AWS_SECRET_ACCESS_KEY=YOUR_SECRET_ACCESS_KEY_HERE
AWS_REGION=us-west-2
```

### 3. Development Environment

#### 3.1. Python Environment
- **Python 3.11 or higher**
- Package manager: `pip`

**Verify installation:**
```bash
python --version
# Expected: Python 3.11.x or higher

pip --version
```

#### 3.2. Node.js Environment
- **Node.js 18+ and npm**
- Required for React frontend

**Verify installation:**
```bash
node --version
# Expected: v18.x.x or higher

npm --version
```

#### 3.3. PostgreSQL Database
- **PostgreSQL 14+ installed locally** or use Docker

**Option 1: Install locally**
- Download from: https://www.postgresql.org/download/
- Create database: `ev_rental_db`

**Option 2: Use Docker**
```bash
docker run -d \
  --name postgres-ev \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=ev_rental_db \
  -p 5432:5432 \
  postgres:14
```
**Verify PostgreSQL:**
```bash
# Check PostgreSQL is running
psql --version

# Connect to database
psql -U postgres -d ev_rental_db
```

### 4. Code Editor & Tools

- **VS Code** or your preferred IDE
- **Git** for cloning repositories
- **Postman** or **cURL** for API testing (optional)

**Install VS Code:**
- Download from: https://code.visualstudio.com/

**Install Git:**
```bash
# macOS
brew install git

# Windows
# Download from: https://git-scm.com/download/win

# Verify
git --version
```

### 5. AWS CLI (Optional)

Install AWS CLI to interact with AWS services from command line:

```bash
# macOS/Linux
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

# Windows
# Download from: https://awscli.amazonaws.com/AWSCLIV2.msi

# Verify
aws --version
```

**Configure AWS CLI:**
```bash
aws configure
# Enter your Access Key ID: AKIA5GPEMGJZK6E7PMEB
# Enter your Secret Access Key: (paste your secret key)
# Default region name: us-west-2
# Default output format: json
```

**Test AWS CLI:**
```bash
# List available Bedrock models
aws bedrock list-foundation-models --region us-west-2

# Check your identity
aws sts get-caller-identity
```

### Prerequisites Checklist

Before proceeding to the next step, ensure you have:

- ✅ AWS Account with Bedrock access in supported region
- ✅ IAM User created with `AmazonBedrockFullAccess` policy
- ✅ Access Key ID and Secret Access Key saved securely
- ✅ Python 3.11+ installed and verified
- ✅ Node.js 18+ and npm installed and verified
- ✅ PostgreSQL 14+ database running
- ✅ Code editor (VS Code recommended) installed
- ✅ Git installed and configured
- ✅ (Optional) AWS CLI installed and configured

### Estimated Costs

This workshop uses the following AWS services:

| Service | Estimated Cost | Notes |
|---------|---------------|-------|
| **AWS Bedrock - Claude 3.5 Sonnet** | ~$0.50 - $2.00 | Pay per API call (input/output tokens) |
| **AWS Bedrock - Knowledge Base** | ~$0.10 - $0.50 | Vector storage + retrieval |
| **S3 Storage** | ~$0.02 | Minimal for documents |
| **Data Transfer** | ~$0.05 | Usually within free tier |
| **Total** | ~$0.67 - $2.57 | For the entire workshop |

💡 **Tip:** Remember to clean up resources after the workshop to avoid ongoing charges!

---

**Next:** Proceed to [Setup AWS Bedrock](../5.3-Setup-Bedrock/) to enable models and create Knowledge Base.