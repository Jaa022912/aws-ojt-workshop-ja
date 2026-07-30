---
title: "Deployment Strategy"
date: 2026-05-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Section 5.4 - Deployment Strategy & Onboarding

This document details the deployment workflow for both the backend serverless infrastructure and the frontend React application, as well as the customer onboarding process.

---

## 1. Backend Serverless Deployment (AWS SAM CLI)

### Step 1: Build Source Code
Compile dependencies inside an Amazon Linux container to ensure binary compatibility with AWS Lambda.

```bash
cd backend
sam build --use-container
```

### Step 2: Deploy CloudFormation Stack
Execute guided deployment to provision API Gateway, Lambda Functions, DynamoDB, EventBridge, and SNS.

```bash
sam deploy --guided
```

Parameters specified during prompt:
- **Stack Name:** `ai-aws-advisor`
- **AWS Region:** `us-east-1` (or matching Bedrock availability region)
- **Confirm changes before deploy:** `Y`
- **Allow SAM CLI IAM role creation:** `Y`
- **Save parameters to configuration file:** `Y` (`samconfig.toml`)

### Step 3: Capture Outputs
Record the generated `ApiGatewayEndpoint` URL output by SAM CLI (e.g., `https://<api-id>.execute-api.us-east-1.amazonaws.com/prod`).

---

## 2. Frontend Deployment & Configuration

### Step 1: Environment Configuration
Create a `.env` file in `frontend/`:

```env
VITE_API_BASE_URL=https://<your-api-id>.execute-api.us-east-1.amazonaws.com/prod
```

### Step 2: Start Local Dev Server
```bash
cd frontend
npm install
npm run dev
```

### Step 3: Production Build
```bash
npm run build
```
Generates minified static assets in `dist/` ready for hosting on Amazon S3 + CloudFront, Vercel, or Netlify.

---

## 3. Customer Account Onboarding

To connect a target AWS account for auditing:

1. Customer logs into their target AWS Account Console.
2. Navigates to **IAM -> Roles -> Create Role**.
3. Selects **AWS Account** trusted entity and enters our SaaS Provider Account ID.
4. Attaches `ReadOnlyAccess` policy to the role.
5. Copies the generated **Role ARN** (`arn:aws:iam::<CustomerAccountID>:role/AIAdvisorAuditRole`).
6. Submits the Role ARN in the AI AWS Advisor dashboard when adding a new Project.
