---
title: "Tổng quan Workshop"
date: 2026-05-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

# Phần 5.1 - Tổng quan Workshop

## Tóm tắt Dự án

**AI AWS Advisor** được thiết kế như một hệ thống B2B SaaS toàn diện cấp doanh nghiệp, có khả năng quét hạ tầng đa tài khoản AWS của khách hàng một cách an toàn, thu thập cấu hình bằng cơ chế phân quyền tạm thời và phân tích bằng Trí tuệ nhân tạo (Generative AI).

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
                                    | Ghi thông tin quét & khuyến nghị
                  +-----------------+-----------------+
                  |   Hourly Scanning Collector Lambda|
                  +--------+----------------+---------+
                           |                |
             sts:AssumeRole|                | Prompt JSON Context
                           v                v
                  +--------+--------+  +----+------------------+
                  |  Tài khoản AWS  |  |   Amazon Bedrock     |
                  |   Khách hàng    |  |  (Claude 3 Haiku)    |
                  +-----------------+  +----------------------+
```

---

## Bài toán Thực tế

Quản lý hệ thống AWS lớn trong môi trường thực tế gặp 3 thách thức lớn:

1. **Lỗi cấu hình Bảo mật tiềm ẩn:** S3 Bucket mở công khai, Security Group mở `0.0.0.0/0`, hay dữ liệu không được mã hóa thường bị bỏ qua cho đến khi xảy ra rò rỉ dữ liệu.
2. **Lãng phí Chi phí Đám mây:** EBS Volume nhàn rỗi, EC2 instance bỏ trống, Elastic IP không gắn vào server làm tiêu tốn hàng nghìn USD hàng tháng.
3. **Quy trình Kiểm toán Thủ công tốn thời gian:** Đội ngũ DevOps và Security phải tốn hàng trăm giờ rà soát thủ công các file JSON cấu hình thô.

---

## Công nghệ Sử dụng

- **Frontend:** React 18, Vite, Tailwind CSS, shadcn/ui, Recharts, TanStack React Query.
- **Backend Serverless:** Python 3.12, AWS Lambda, Amazon API Gateway, Amazon EventBridge, Amazon SNS.
- **Trí tuệ Nhân tạo (GenAI):** Amazon Bedrock (Anthropic Claude 3 Haiku `anthropic.claude-3-haiku-20240307-v1:0`).
- **Cơ sở dữ liệu:** Amazon DynamoDB (Thiết kế Single-Table NoSQL).
- **Bảo mật:** AWS Security Token Service (STS `sts:AssumeRole`) phân quyền cross-account.
- **IaC:** AWS Serverless Application Model (SAM CLI).
