---
title: "Worklog Tuần 9"
date: 2026-07-12
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Triển khai Grafana Dashboard; Sử dụng AWS Tag & Resource Groups để quản lý và phân quyền tài nguyên (ABAC); Quản lý hệ thống tập trung với AWS Systems Manager (Patch Manager, Session Manager) và giới thiệu CloudFormation (IaC).

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu Grafana và vai trò trực quan hóa dữ liệu giám sát <br> - Cài đặt Grafana trên EC2 và kết nối với CloudWatch làm nguồn dữ liệu <br> - Xây dựng Dashboard để theo dõi Metrics (CPU, Memory, Disk, Network) theo thời gian thực | 13/07/2026 | 13/07/2026 | <https://000029.awsstudygroup.com/vi/> |
| 3   | - Nghiên cứu AWS Tag và AWS Resource Groups <br> - Thực hành gán Tag cho EC2, EBS và tạo Resource Group dựa trên Tag để phân loại và quản lý tài nguyên tập trung theo dự án/môi trường | 14/07/2026 | 14/07/2026 | <https://000027.awsstudygroup.com/vi/> |
| 4   | - Thực hành quản lý quyền truy cập EC2 bằng IAM kết hợp Resource Tag (ABAC - Tag-based Access Control) <br> - Tạo IAM Policy có điều kiện dựa trên Tag để phân quyền theo nguyên tắc Least Privilege | 15/07/2026 | 15/07/2026 | <https://000028.awsstudygroup.com/vi/> |
| 5   | - Nghiên cứu AWS Systems Manager (SSM) <br> - Cấu hình Patch Manager để quản lý và tự động triển khai bản vá cho EC2 <br> - Sử dụng Run Command để thực thi lệnh từ xa trên nhiều máy chủ đồng thời mà không cần SSH | 16/07/2026 | 16/07/2026 | <https://000031.awsstudygroup.com/vi/> |
| 6   | - Thực hành kết nối an toàn đến Public/Private EC2 qua SSM Session Manager (không mở port 22) <br> - Cấu hình Port Forwarding qua Session Manager <br> - Nghiên cứu AWS CloudFormation để tự động triển khai hạ tầng dưới dạng mã (IaC) <br> - Dọn dẹp tài nguyên | 17/07/2026 | 17/07/2026 | <https://000058.awsstudygroup.com/vi/> |

### Kết quả đạt được tuần 9:

* Biết cách cài đặt Grafana trên EC2, kết nối CloudWatch và thiết lập biểu đồ trực quan.
* Nắm được tầm quan trọng của Tagging và Resource Groups trong quản trị hệ thống Cloud.
* Hiểu cách phân quyền linh hoạt bằng Tag-Based Access Control (ABAC) trong IAM.
* Nắm vững tính năng Patch Manager, Run Command và Session Manager của Systems Manager để quản trị máy chủ an toàn.
* Hiểu khái niệm Infrastructure as Code (IaC) và cấu hình template cơ bản của CloudFormation.
