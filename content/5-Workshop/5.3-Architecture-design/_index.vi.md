---
title: "Kiến trúc & Thiết kế"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

# Phần 5.3 - Kiến trúc & Thiết kế Kỹ thuật

Dự án **AI AWS Advisor** được phát triển trên 3 trụ cột kỹ thuật chính: **Kiến trúc Serverless**, **Bảo mật Zero-Trust**, và **Generative AI**.

---

## 1. Kiến trúc Tổng quan Hệ thống

Hệ thống phân chia ranh giới bảo mật thành 3 vùng độc lập:

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
    
    subgraph Target ["Tài khoản AWS Khách hàng"]
        STS["AWS STS (AssumeRole)"]
        Resources["Tài nguyên Khách hàng (EC2, S3, IAM...)"]
    end

    User -->|HTTPS Request| APIGW
    APIGW --> Lambdas
    Lambdas -->|Đọc / Ghi| DDB
    Lambdas -->|Truy vấn| Bedrock

    Event -->|Kích hoạt| Collector
    Collector -->|Ghi Dữ liệu| DDB
    Collector -->|Gửi Prompt| Bedrock
    Collector -->|Gửi Cảnh báo| SNS

    Collector -->|sts:AssumeRole| STS
    STS -->|Lấy Cấu hình| Resources
```

---

## 2. Bảo mật Zero-Trust (Cross-Account Delegation)

Thay vì yêu cầu khách hàng cung cấp Access Key / Secret Key cố định (nguy cơ rò rỉ rất cao), hệ thống áp dụng cơ chế ủy quyền ủy thác qua AWS STS:

```mermaid
graph LR
    subgraph Provider ["Tài khoản SaaS Provider"]
        L["Collector Lambda"]
    end

    subgraph Customer ["Tài khoản AWS Khách hàng"]
        IAM["Cross-Account IAM Role (Read-Only)"]
        STS["AWS Security Token Service (STS)"]
        EC2["Amazon EC2"]
        S3["Amazon S3"]
    end

    L -->|1. sts:AssumeRole| STS
    STS -->|2. Xác thực Trust Policy| IAM
    IAM -.->|3. Cấp Session Token| STS
    STS -->|4. Trả về Temp Credentials| L
    
    L -->|5. Gọi API kiểm toán bằng Temp Token| EC2
    L -->|5. Gọi API kiểm toán bằng Temp Token| S3
```

---

## 3. Luồng Quét Tự động & Phân tích Trí tuệ Nhân tạo

```mermaid
sequenceDiagram
    participant EB as Amazon EventBridge
    participant Collector as Collector Lambda
    participant STS as AWS STS
    participant Target as Tài khoản Khách hàng
    participant DDB as Amazon DynamoDB
    participant AI as Amazon Bedrock (Claude 3)
    participant SNS as Amazon SNS

    EB->>Collector: Kích hoạt (Mỗi 1 giờ)
    Collector->>DDB: Lấy danh sách dự án active
    DDB-->>Collector: Danh sách Projects (Role ARNs)
    
    loop Cho mỗi Project
        Collector->>STS: sts:AssumeRole (Role ARN)
        STS-->>Collector: Temporary Credentials
        Collector->>Target: Quét cấu hình (boto3)
        Target-->>Collector: Cấu hình thô JSON & Metrics
        Collector->>DDB: Lưu tài nguyên thô
        Collector->>AI: Tạo Prompt (Security, Cost)
        AI-->>Collector: Kết quả Khuyến nghị JSON
        Collector->>DDB: Lưu Insights
        
        opt Có rủi ro nghiêm trọng?
            Collector->>SNS: Phát tin nhắn Cảnh báo
            SNS-->>Customer: Gửi Email cho Khách hàng
        end
    end
```

---

## 4. Cơ sở Dữ liệu DynamoDB Single-Table Design

Mô hình thiết kế NoSQL linh hoạt hỗ trợ đa đối tượng:

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
