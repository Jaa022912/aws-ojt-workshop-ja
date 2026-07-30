---
title: "Prerequisites & Setup"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Section 5.2 - System Requirements & Prerequisites

To deploy, operate, and contribute to **AI AWS Advisor**, ensure your local development machine and AWS accounts meet the following requirements.

---

## 1. AWS Account & Service Entitlements

- **AWS Account:** Requires Administrator Access privileges (`AdministratorAccess`).
- **Amazon Bedrock Model Access:**
  - `Claude 3 Haiku` model access must be explicitly enabled in `us-east-1` or `ap-southeast-1` via the AWS Bedrock Console (**Bedrock -> Model access -> Request access**).
  - Target Model ID / ARN: `anthropic.claude-3-haiku-20240307-v1:0`.
- **AWS CLI v2:** Installed and configured (`aws configure`) with valid credentials.

---

## 2. Serverless Backend Toolchain

- **AWS SAM CLI:** Used to build, package, and deploy the serverless infrastructure (`template.yaml`).
- **Python 3.12+:** Primary runtime language for Lambda API Handlers and AI Analyzers.
- **Docker Desktop:** Required by SAM CLI (`sam build --use-container`) to compile dependencies inside Amazon Linux 2023 container environments.

---

## 3. Frontend & Local Emulation Toolchain

- **Node.js (v18.0 or higher):** Runtime for React/Vite development.
- **npm / pnpm / yarn:** JavaScript package manager.
- **DynamoDB Local:** Supported via Docker Compose (`amazon/dynamodb-local`) for offline development without modifying cloud databases.

```bash
# Verify local toolchain installations
aws --version
sam --version
python --version
node --version
docker --version
```