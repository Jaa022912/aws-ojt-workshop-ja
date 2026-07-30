---
title: "Chiến lược Triển khai"
date: 2026-05-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

# Phần 5.4 - Chiến lược Triển khai & Tích hợp Khách hàng

Tài liệu này chi tiết quy trình triển khai hạ tầng Backend Serverless, ứng dụng Frontend React và các bước tích hợp tài khoản AWS của khách hàng vào hệ thống.

---

## 1. Triển khai Backend Serverless (AWS SAM CLI)

### Bước 1: Biên dịch Mã nguồn
Biên dịch thư viện phụ thuộc bên trong container Amazon Linux để đảm bảo tính tương thích binary với AWS Lambda.

```bash
cd backend
sam build --use-container
```

### Bước 2: Triển khai CloudFormation Stack
Thực hiện triển khai theo hướng dẫn để khởi tạo API Gateway, Lambda Functions, DynamoDB, EventBridge và SNS.

```bash
sam deploy --guided
```

Các tham số chính:
- **Stack Name:** `ai-aws-advisor`
- **AWS Region:** `us-east-1` (hoặc region hỗ trợ Amazon Bedrock)
- **Confirm changes before deploy:** `Y`
- **Allow SAM CLI IAM role creation:** `Y`
- **Save parameters to configuration file:** `Y` (`samconfig.toml`)

### Bước 3: Lưu lại Đầu ra Outputs
Ghi lại URL `ApiGatewayEndpoint` được xuất ra từ SAM CLI (ví dụ: `https://<api-id>.execute-api.us-east-1.amazonaws.com/prod`).

---

## 2. Triển khai Frontend React Application

### Bước 1: Cấu hình Môi trường
Tạo file `.env` tại thư mục `frontend/`:

```env
VITE_API_BASE_URL=https://<your-api-id>.execute-api.us-east-1.amazonaws.com/prod
```

### Bước 2: Chạy Server Phát triển
```bash
cd frontend
npm install
npm run dev
```

### Bước 3: Đóng gói Sản phẩm
```bash
npm run build
```
Tạo mã nguồn tĩnh trong thư mục `dist/` sẵn sàng tải lên Amazon S3 + CloudFront, Vercel hoặc Netlify.

---

## 3. Quy trình Tích hợp Tài khoản Khách hàng

Các bước khách hàng thực hiện để kết nối tài khoản AWS cần kiểm toán:

1. Khách hàng đăng nhập vào AWS Console của tài khoản cần kiểm toán.
2. Truy cập **IAM -> Roles -> Create Role**.
3. Chọn loại Trusted Entity là **AWS Account** và nhập Account ID của tài khoản SaaS Provider.
4. Gắn policy `ReadOnlyAccess` cho IAM Role.
5. Sao chép **Role ARN** được tạo ra (`arn:aws:iam::<CustomerAccountID>:role/AIAdvisorAuditRole`).
6. Nhập Role ARN này trên Dashboard của AI AWS Advisor để khởi tạo Dự án.
