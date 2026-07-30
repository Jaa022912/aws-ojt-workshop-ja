---
title: "Workshop Overview"
date: 2026-05-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Section 5.1 - Workshop Overview

## Executive Summary

**AI AWS Advisor** is designed as a full-stack, enterprise-grade B2B SaaS platform that seamlessly scans customer multi-account AWS environments, collects resource configurations safely using temporary delegation, and delivers generative AI-powered optimization insights.

```
                  +-----------------------------------+
                  |      Enterprise Web Dashboard     |
                  |     (React 18 + Vite + Tailwind)  |
                  +-----------------+-----------------+
                                    | HTTPS / REST
                                    v
                  +-----------------+-----------------+
                  |       Amazon API Gateway         |
                  +-----------------+-----------------+
                                    |
            +-----------------------+-----------------------+
            |                       |                       |
            v                       v                       v
    +---------------+       +---------------+       +---------------+
    | Project API   |       | Insights API  |       | Chat Copilot  |
    | Lambda Handler|       | Lambda Handler|       | Lambda Handler|
    +-------+-------+       +-------+-------+       +-------+-------+
            |                       |                       |
            +-----------------------+-----------------------+
                                    |
                                    v
                       +------------+------------+
                       |   Amazon DynamoDB       |
                       |  (Single-Table NoSQL)   |
                       +------------+------------+
                                    ^
                                    | Write Scanned Resources & Insights
                  +-----------------+-----------------+
                  |   Hourly Scanning Collector Lambda|
                  +--------+----------------+---------+
                           |                |
             sts:AssumeRole|                | Prompt JSON Context
                           v                v
                  +--------+--------+  +----+------------------+
                  |  Target Customer|  |   Amazon Bedrock     |
                  |    AWS Account  |  |  (Claude 3 Haiku)    |
                  +-----------------+  +----------------------+
```

---

## Core Problem Statement

Managing modern AWS infrastructure across dynamic development, staging, and production environments presents critical challenges for CloudOps and Security teams:

1. **Hidden Security Misconfigurations:** Publicly exposed S3 buckets, permissive security group rules (`0.0.0.0/0`), and unencrypted volumes often go unnoticed until a data breach occurs.
2. **Cloud Resource Waste:** Unattached EBS volumes, idle EC2 instances, and unused Elastic IPs accumulate thousands of dollars in unnecessary monthly bills.
3. **Manual Audit Friction:** Security officers and DevOps engineers spend hundreds of hours manually reviewing AWS Trusted Advisor and raw JSON describe API calls.

---

## Technology Stack

- **Frontend Application:** React 18, Vite, Tailwind CSS, shadcn/ui, Recharts, TanStack React Query.
- **Serverless Backend:** Python 3.12, AWS Lambda, Amazon API Gateway, Amazon EventBridge, Amazon SNS.
- **Artificial Intelligence (GenAI):** Amazon Bedrock (Anthropic Claude 3 Haiku model `anthropic.claude-3-haiku-20240307-v1:0`).
- **Database & Storage:** Amazon DynamoDB (Single-Table NoSQL Design).
- **Security Framework:** AWS Security Token Service (STS `sts:AssumeRole`) for cross-account delegation.
- **Infrastructure as Code (IaC):** AWS Serverless Application Model (SAM CLI).