---
title: "Architecture & Design"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Section 5.3 - Architecture & Technical Design

The **AI AWS Advisor** project is built upon three core technological pillars: **Serverless Computing**, **Zero-Trust Security**, and **Generative AI**.

---

## 1. High-Level Architecture

The system is partitioned into three independent security boundaries:

```mermaid
graph TD
    subgraph Frontend ["Client Frontend (React 18 + Vite)"]
        User["React Dashboard (Vite, Tailwind, Recharts)"]
    end
    
    subgraph Backend ["AI Advisor Backend (Serverless Stack)"]
        APIGW["Amazon API Gateway (REST API)"]
        DDB["Amazon DynamoDB (Single-Table NoSQL)"]
        Lambdas["AWS Lambda (API Handlers)"]
        Collector["AWS Lambda (Data Collector)"]
        Event["Amazon EventBridge (Cron 1 Hour)"]
        Bedrock["Amazon Bedrock (Claude 3 Haiku)"]
        SNS["Amazon SNS (Email Alerts)"]
    end
    
    subgraph Target ["Customer Target AWS Accounts"]
        STS["AWS STS (AssumeRole)"]
        Resources["Customer Resources (EC2, S3, IAM...)"]
    end

    User -->|HTTPS Request| APIGW
    APIGW --> Lambdas
    Lambdas -->|Read / Write| DDB
    Lambdas -->|Query| Bedrock

    Event -->|Trigger| Collector
    Collector -->|Write Data| DDB
    Collector -->|Analyze Prompt| Bedrock
    Collector -->|Publish Alert| SNS

    Collector -->|sts:AssumeRole| STS
    STS -->|Fetch Config| Resources
```

### Design Decision: 100% Serverless
Operating on AWS Lambda, API Gateway, and DynamoDB eliminates baseline 24/7 EC2 infrastructure costs, granting zero idle costs and instant scalability.

---

## 2. Zero-Trust Security (Cross-Account Delegation)

Instead of storing customer permanent AWS Access Keys (which introduces massive security risks), the application requires customers to provision a Read-Only IAM Role that trusts our SaaS account.

```mermaid
graph LR
    subgraph Provider ["SaaS Provider Account"]
        L["Collector Lambda"]
    end

    subgraph Customer ["Customer AWS Account"]
        IAM["Cross-Account IAM Role (Read-Only)"]
        STS["AWS Security Token Service (STS)"]
        EC2["Amazon EC2"]
        S3["Amazon S3"]
    end

    L -->|1. sts:AssumeRole| STS
    STS -->|2. Validates Trust Policy| IAM
    IAM -.->|3. Grants Session Token| STS
    STS -->|4. Returns Temp Credentials| L
    
    L -->|5. Audit API Calls| EC2
    L -->|5. Audit API Calls| S3
```

---

## 3. Automated Scanning & AI Analysis Flow

```mermaid
sequenceDiagram
    participant EB as Amazon EventBridge
    participant Collector as Collector Lambda
    participant STS as AWS STS
    participant Target as Target AWS Account
    participant DDB as Amazon DynamoDB
    participant AI as Amazon Bedrock (Claude 3)
    participant SNS as Amazon SNS

    EB->>Collector: Trigger (Every 1 hour)
    Collector->>DDB: Fetch active projects
    DDB-->>Collector: List of Projects (Role ARNs)
    
    loop For each Project
        Collector->>STS: sts:AssumeRole (Role ARN)
        STS-->>Collector: Temporary Credentials
        Collector->>Target: Fetch configurations (boto3)
        Target-->>Collector: Raw JSON configs & metrics
        Collector->>DDB: Save raw resources
        Collector->>AI: Prepare context & Prompt (Security, Cost)
        AI-->>Collector: AI Insights JSON Response
        Collector->>DDB: Store Security, Cost, Performance Insights
        
        opt Has Critical Risks?
            Collector->>SNS: Publish Alert Message
            SNS-->>Customer: Send Email Notification
        end
    end
```

---

## 4. DynamoDB NoSQL Single-Table Design

The application utilizes Amazon DynamoDB with a Single-Table / Multi-Entity design pattern:

```mermaid
classDiagram
    class PROJECTS {
        +string project_id PK
        +string sk SK
        +string project_name
        +string role_arn
        +string region
    }
    class RESOURCES {
        +string project_id PK
        +string resource_id SK
        +string resource_type
        +json raw_data
    }
    class INSIGHTS {
        +string project_id PK
        +string insight_id SK
        +string severity
        +string recommendation
    }
    PROJECTS "1" -- "many" RESOURCES : owns
    PROJECTS "1" -- "many" INSIGHTS : generates
```

- **PROJECTS:** `PK: project_id`, `SK: METADATA`
- **RESOURCES:** `PK: project_id`, `SK: RESOURCE#<id>`
- **INSIGHTS:** `PK: project_id`, `SK: INSIGHT#<id>`
- **ALERTS:** `PK: project_id`, `SK: ALERT#<id>`

This design provides strict tenant isolation (`project_id` Partition Key) and zero relational migration friction for dynamic AWS JSON configuration schemas.
