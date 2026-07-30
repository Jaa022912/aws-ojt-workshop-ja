---
title: "Blog 3"
date: 2026-07-28
weight: 3
chapter: false
pre: "<b>3.3.</b>"
---

# Modernizing KYC with Serverless & Agentic AI – A Critical Review

## Introduction

While exploring modern cloud architectures for the financial industry, I came across an article on the **AWS Architecture Blog** describing how IBM and AWS modernize the **Know Your Customer (KYC)** process using **Serverless**, **Agentic AI**, **Event-Driven Architecture**, and several AWS managed services.

What caught my attention was not only the use of AI to automate customer onboarding, but also how multiple specialized AI agents collaborate to perform identity verification, document analysis, fraud detection, and compliance assessment.

Although the proposed architecture is technically impressive, I believe there are still several aspects that deserve further discussion, particularly regarding security, regulatory compliance, operational cost, and real-world deployment.

---

## What is KYC?

**Know Your Customer (KYC)** is a mandatory process that financial institutions use to verify the identity of their customers before providing banking or financial services.

The primary objectives of KYC include:

- Verifying customer identity
- Checking sanctions and watch lists
- Assessing customer risk
- Detecting suspicious activities
- Maintaining audit trails for regulatory compliance

Traditional KYC systems are often batch-oriented and rely heavily on manual verification, causing customer onboarding to take several days.

---

## The Architecture Proposed by AWS and IBM

The proposed solution adopts an **Event-Driven Architecture** combined with **Agentic AI** to automate and accelerate the KYC workflow.

The primary AWS services include:

- Amazon MSK
- AWS Lambda
- Amazon Bedrock
- Amazon OpenSearch Serverless
- Amazon S3
- Amazon DynamoDB
- AgentCore Gateway
- Amazon CloudWatch
- AWS Identity and Access Management (IAM)

Within this architecture:

- **Amazon MSK** receives and distributes KYC-related events.
- A **Supervisor Agent** orchestrates the overall workflow.
- Multiple specialized AI agents handle different business tasks.
- A **Knowledge Base** powered by OpenSearch Serverless and Amazon S3 provides Retrieval-Augmented Generation (RAG).
- **AgentCore Gateway** integrates cloud services with existing on-premises banking systems.

![Overall Architecture of Modernizing KYC with Serverless & Agentic AI](kyc-agentic-ai-architecture.png)

*Figure 1. Overall architecture of the KYC platform built with Event-Driven Architecture and Agentic AI.*

The architecture illustrates how every customer onboarding request is transformed into an event and processed asynchronously.

Once a KYC request is received through **Amazon MSK**, the **Supervisor Agent** coordinates the execution of several specialized AI agents.

Each agent focuses on a specific responsibility:

- **Identity Verification Agent** performs identity validation and third-party verification.
- **Document Analysis Agent** extracts and analyzes information from submitted documents using OCR.
- **Fraud Detection Agent** detects suspicious behaviors and potential fraud.
- **Compliance & Risk Agent** evaluates regulatory compliance and customer risk.
- **Customer Experience Agent** optimizes the onboarding workflow and customer interactions.

Throughout the process, the agents retrieve regulatory information and organizational policies from a centralized **Knowledge Base** using **Retrieval-Augmented Generation (RAG)** before making decisions.

Finally, results are delivered back to core banking systems through **AgentCore Gateway**.

---

## Architecture Highlights

### Event-Driven Architecture with Amazon MSK

One of the strongest design decisions is adopting **Amazon Managed Streaming for Apache Kafka (Amazon MSK)** as the event backbone.

Instead of processing KYC requests in nightly batches, every onboarding request becomes an independent event.

This approach offers several advantages:

- Near real-time processing
- Faster customer onboarding
- Independent scaling of individual services
- Better fault isolation through service decoupling

---

### Multi-Agent Orchestration

Rather than relying on a single AI model, the solution divides responsibilities across multiple specialized agents.

A **Supervisor Agent** coordinates these agents and aggregates their outputs before making a final decision.

The decision flow is illustrated below:

```text
Confidence > 95%
        │
        ▼
 Auto Approval

Confidence 75–95%
        │
        ▼
 Additional Verification

Confidence <75%
        │
        ▼
 Human Review
```

This modular approach makes the system easier to maintain and extend as business requirements evolve.

---

### Retrieval-Augmented Generation (RAG)

Financial regulations change frequently.

Instead of relying solely on a pretrained Large Language Model, the architecture employs **Retrieval-Augmented Generation (RAG)**.

The Knowledge Base is implemented using:

- Amazon OpenSearch Serverless
- Amazon S3

Before making decisions, AI agents retrieve the latest regulations, policies, and documentation, reducing the likelihood of hallucinations and outdated responses.

---

### AgentCore Gateway

Many financial institutions still operate mission-critical banking systems on-premises.

AgentCore Gateway enables secure integration between cloud-native AI services and legacy enterprise systems such as:

- Core Banking Systems
- Customer Management Systems
- Risk & AML Platforms
- Third-party Verification APIs

This hybrid approach allows organizations to modernize their workflows without replacing existing infrastructure.

---

## Challenges and Open Questions

Although the proposed architecture is promising, several important questions remain unanswered.

### Handling Complex KYC Scenarios

The article claims that KYC requests can be completed in less than five minutes.

However, it does not discuss more complicated cases, including:

- Politically Exposed Persons (PEPs)
- Dual citizenship
- Rare jurisdictions
- Missing documentation
- Complex corporate ownership structures

These scenarios often require extensive human review and significantly longer processing times.

---

### Explainable AI

The article briefly mentions explainable AI but provides very limited implementation details.

Several important questions remain:

- Why did the AI reach a particular decision?
- Can auditors reproduce or verify the reasoning?
- Does the explanation satisfy regulations such as the EU AI Act or MAS FEAT Principles?

These capabilities are essential for AI systems operating in highly regulated industries.

---

### Security Considerations

The article also provides limited discussion regarding modern AI security threats.

Potential attack vectors include:

- Deepfake identity documents
- Synthetic identities
- Adversarial attacks against AI models
- Prompt injection targeting AI agents

As Agentic AI becomes increasingly common, these risks deserve far more attention.

---

### Cost Considerations

Although serverless architectures reduce infrastructure management, operational costs can become significant at enterprise scale.

Organizations should carefully evaluate the costs associated with:

- Amazon MSK
- AWS Lambda
- Amazon Bedrock
- Amazon OpenSearch Serverless

Additional expenses may include:

- Legacy system migration
- Compliance assessments
- Penetration testing
- AI model monitoring
- Security audits

These costs are often overlooked during architectural discussions.

---

## What I Learned

After reading this article, I realized that building a modern KYC platform involves much more than simply adding AI.

Several architectural concepts stood out:

- Event-Driven Architecture is well suited for high-volume distributed workflows.
- Multi-Agent systems simplify complex business processes by assigning specialized responsibilities.
- Retrieval-Augmented Generation enables AI to use the latest regulatory information instead of relying solely on pretrained knowledge.
- Explainability and Human-in-the-Loop remain essential for compliance-sensitive applications.
- A successful architecture must balance performance, security, scalability, governance, and regulatory compliance.

---

## Conclusion

The **Modernizing KYC with Serverless & Agentic AI** architecture provides an excellent reference for designing intelligent, cloud-native financial systems.

Technologies such as Amazon MSK, AWS Lambda, Amazon Bedrock, and Retrieval-Augmented Generation demonstrate how serverless computing and AI can significantly improve customer onboarding.

However, technical innovation alone is not sufficient.

Real-world financial systems must also address explainability, security, disaster recovery, operational costs, and legal accountability before AI can safely automate critical business decisions.

Overall, this architecture is an excellent learning resource for anyone interested in cloud architecture, generative AI, and modern financial systems on AWS.

---

# References

## Original Article

**Modernizing KYC with Serverless & Agentic AI**

https://aws.amazon.com/blogs/architecture/modernizing-kyc-with-serverless-agentic-ai/

---

## AWS Lambda Documentation

https://docs.aws.amazon.com/lambda/

---

## Amazon Bedrock Documentation

https://docs.aws.amazon.com/bedrock/

---

## Amazon MSK Documentation

https://docs.aws.amazon.com/msk/

---

## Amazon OpenSearch Serverless Documentation

https://docs.aws.amazon.com/opensearch-service/latest/developerguide/serverless.html

---

# Related AWS Services

- Amazon MSK
- AWS Lambda
- Amazon Bedrock
- Amazon OpenSearch Serverless
- Amazon S3
- Amazon DynamoDB
- Amazon CloudWatch
- AWS Identity and Access Management (IAM)
- AgentCore Gateway

## Related Articles

- **Facebook:** [Modernizing KYC with Serverless & Agentic AI](https://www.facebook.com/groups/660548818043427/user/61580015957889/)
---

# Sources

1. AWS Architecture Blog. *Modernizing KYC with Serverless & Agentic AI.*

2. AWS Documentation. *Amazon MSK.*

3. AWS Documentation. *Amazon Bedrock.*

4. AWS Documentation. *AWS Lambda.*

5. AWS Documentation. *Amazon OpenSearch Serverless.*