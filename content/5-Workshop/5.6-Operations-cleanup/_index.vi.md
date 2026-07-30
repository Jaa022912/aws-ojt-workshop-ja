---
title: "Vận hành & Dọn dẹp"
date: 2026-05-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Phần 5.6 - Vận hành, Dọn dẹp Tài nguyên & Đánh giá Kiến trúc

Tài liệu này hướng dẫn quy trình tiêu hủy tài nguyên hệ thống an toàn, đồng thời tổng kết các bài học kiến trúc và định hướng phát triển cho **AI AWS Advisor**.

---

## 1. Tiêu hủy Tài nguyên Cloud Tự động

Do toàn bộ hạ tầng Backend được quản lý dưới dạng mã (IaC) qua AWS SAM CLI, việc dọn dẹp tài nguyên được thực hiện hoàn toàn tự động.

Để xóa CloudFormation stack và giải phóng tất cả Lambda functions, API Gateway, EventBridge rules và DynamoDB tables:

```bash
cd backend
sam delete
```

Xác nhận việc xóa khi được hỏi tên stack (`ai-aws-advisor`).

---

## 2. Danh mục Kiểm tra Sau khi Dọn dẹp

- **Amazon CloudWatch Log Groups:** Kiểm tra và xóa thủ công các nhóm log có tiền tố `/aws/lambda/ai-aws-advisor-*` để tránh chi phí lưu trữ tích lũy.
- **Thu hồi Customer IAM Role:** Xóa các IAM Role ủy quyền (`AIAdvisorAuditRole`) trên các tài khoản AWS của khách hàng.

---

## 3. Tổng kết Kiến trúc & Bài học Kinh nghiệm

1. **Mô hình Bảo mật Zero-Trust:** Áp dụng `sts:AssumeRole` giúp loại bỏ hoàn toàn nguy cơ rò rỉ Access Key dài hạn, đáp ứng các tiêu chuẩn tuân thủ doanh nghiệp (SOC2 / ISO27001).
2. **Tối ưu Chi phí với Serverless:** Sử dụng AWS Lambda và DynamoDB Single-Table Design giúp chi phí duy trì hệ thống ở mức $0/tháng khi nhàn rỗi.
3. **AI là Động cơ Vận hành:** Amazon Bedrock (Claude 3 Haiku) chứng minh LLM hoạt động cực kỳ hiệu quả như một công cụ phân tích cấu hình thô thành dữ liệu cấu trúc JSON chuẩn.

---

## 4. Hướng Phát triển Tương lai

- **Xử lý Sự kiện Real-time:** Chuyển từ quét định kỳ theo giờ sang xử lý luồng sự kiện CloudTrail theo thời gian thực qua EventBridge Event Bus.
- **Tự động Sửa lỗi (Autopilot):** Thêm quyền ghi có kiểm soát để AI Advisor tự động sửa lỗi (ví dụ: tự động bật mã hóa cho S3 bucket).
- **Quản lý Định danh:** Tích hợp Amazon Cognito để quản lý xác thực người dùng và phân quyền RBAC.
