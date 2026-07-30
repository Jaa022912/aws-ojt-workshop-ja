---
title: "Kiểm thử & Chất lượng"
date: 2026-05-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

# Phần 5.5 - Kiểm thử & Đảm bảo Chất lượng

Để đảm bảo tính tin cậy cao, độ an toàn và toàn vẹn dữ liệu cho **AI AWS Advisor**, dự án áp dụng kiến trúc kiểm thử tự động 2 lớp độc lập.

---

## 1. Môi trường Kiểm thử Backend (Pytest + Moto)

Backend sử dụng `pytest` kết hợp với thư viện giả lập môi trường AWS (`moto`) để kiểm thử logic nghiệp vụ mà không phát sinh chi phí hay gọi đến API thật.

### Công nghệ sử dụng:
- **`pytest` & `pytest-mock`:** Khung kiểm thử và giả lập hàm fixture.
- **`moto`:** Chặn các cuộc gọi `boto3` AWS SDK, tạo cơ sở dữ liệu DynamoDB ảo chạy trên bộ nhớ RAM.
- **Giả lập Bedrock:** Chặn hàm `invoke_model()` của Bedrock để trả về phản hồi JSON chuẩn, kiểm thử khả năng xử lý dữ liệu AI và xử lý lỗi.

```bash
cd backend
python -m pytest tests/ -v
```

---

## 2. Môi trường Kiểm thử Frontend (Vitest + React Testing Library)

Ứng dụng React áp dụng kiểm thử giao diện tập trung vào trải nghiệm người dùng và hiển thị dữ liệu biểu đồ.

### Công nghệ sử dụng:
- **`Vitest`:** Khung kiểm thử tốc độ cao tích hợp sẵn với Vite.
- **`React Testing Library (RTL)`:** Render các component trên DOM ảo (`jsdom`).
- **`vi.mock()`:** Chặn các lệnh gọi API từ TanStack React Query và Axios.

```bash
cd frontend
npm run test
```

---

## 3. Sẵn sàng cho CI/CD Pipeline

Cả hai bộ unit test đều hoàn thành dưới 10 giây mà không phụ thuộc internet hay tài nguyên cloud, sẵn sàng tích hợp vào **GitHub Actions** hoặc **AWS CodePipeline**.
