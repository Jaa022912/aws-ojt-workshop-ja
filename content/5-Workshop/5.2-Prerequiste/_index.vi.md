---
title: "Yêu cầu & Chuẩn bị"
date: 2026-05-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

# Phần 5.2 - Yêu cầu Hệ thống & Môi trường

Để triển khai và vận hành hệ thống **AI AWS Advisor**, môi trường phát triển và tài khoản AWS cần đáp ứng các điều kiện tiên quyết sau.

---

## 1. Yêu cầu Tài khoản AWS & Quyền Dịch vụ

- **Tài khoản AWS:** Cần có quyền Quản trị viên (`AdministratorAccess`).
- **Quyền Truy cập Amazon Bedrock Model:**
  - Mô hình `Claude 3 Haiku` phải được kích hoạt tại region `us-east-1` hoặc `ap-southeast-1` trên AWS Console (**Bedrock -> Model access -> Request access**).
  - Model ID / ARN: `anthropic.claude-3-haiku-20240307-v1:0`.
- **AWS CLI v2:** Đã cài đặt và cấu hình lệnh (`aws configure`).

---

## 2. Công cụ Backend Serverless

- **AWS SAM CLI:** Bộ công cụ đóng gói và triển khai cơ sở hạ tầng dưới dạng mã (IaC - `template.yaml`).
- **Python 3.12+:** Ngôn ngữ lập trình chính cho các API Handlers và AI Analyzer trên AWS Lambda.
- **Docker Desktop:** Cần thiết cho SAM CLI (`sam build --use-container`) để biên dịch mã nguồn tương thích với môi trường Amazon Linux 2023 của Lambda.

---

## 3. Công cụ Frontend & Giả lập Môi trường

- **Node.js (v18.0 trở lên):** Môi trường thực thi cho dự án React 18 / Vite.
- **npm / pnpm / yarn:** Trình quản lý thư viện Node.js.
- **DynamoDB Local:** Giả lập DynamoDB offline qua Docker Compose (`amazon/dynamodb-local`) để phát triển không cần chạm vào DB thật trên cloud.

```bash
# Kiểm tra phiên bản các công cụ
aws --version
sam --version
python --version
node --version
docker --version
```