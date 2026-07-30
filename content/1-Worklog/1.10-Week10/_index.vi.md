---
title: "Worklog Tuần 10"
date: 2026-07-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Quản lý truy cập tập trung với IAM Identity Center, giới hạn quyền nâng cao bằng Permission Boundary và IAM Role Conditions; Giám sát an ninh hệ thống với AWS Security Hub và AWS WAF.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu AWS IAM Identity Center (Single Sign-On) <br> - Cấu hình truy cập AWS CLI thông qua IAM Identity Center, quản lý định danh và phân quyền truy cập tập trung trên nhiều tài khoản AWS | 20/07/2026 | 20/07/2026 | <https://000012.awsstudygroup.com/vi/> |
| 3   | - Cấu hình Time-based Access Control để giới hạn quyền truy cập theo thời gian <br> - Nghiên cứu IAM Permission Boundary để giới hạn quyền tối đa cho IAM User/Role và ngăn chặn Privilege Escalation (leo thang đặc quyền) | 21/07/2026 | 21/07/2026 | <https://000030.awsstudygroup.com/vi/> |
| 4   | - Ôn tập các khái niệm nâng cao của IAM: Group, Policy, Role và cơ chế Assume Role <br> - Cấu hình IAM Role Conditions để giới hạn quyền truy cập theo địa chỉ IP nguồn và thời gian | 22/07/2026 | 22/07/2026 | <https://000044.awsstudygroup.com/vi/> |
| 5   | - Nghiên cứu AWS Security Hub trong việc quản lý tập trung các cảnh báo bảo mật <br> - Kích hoạt Security Hub, tích hợp với các dịch vụ bảo mật (GuardDuty, Inspector, Macie) và đánh giá mức độ tuân thủ theo các Security Standards | 23/07/2026 | 23/07/2026 | <https://000018.awsstudygroup.com/vi/> |
| 6   | - Nghiên cứu AWS Web Application Firewall (AWS WAF) <br> - Tạo Web ACL, cấu hình các AWS Managed Rules (SQLi, XSS) và Custom Rules để bảo vệ ứng dụng web tích hợp trên ALB/CloudFront <br> - Dọn dẹp tài nguyên | 24/07/2026 | 24/07/2026 | <https://000026.awsstudygroup.com/vi/> |

### Kết quả đạt được tuần 10:

* Hiểu cách quản lý người dùng và Permission Sets tập trung thông qua IAM Identity Center.
* Nắm được cơ chế hoạt động của Permission Boundary và vai trò ngăn chặn leo thang đặc quyền.
* Thiết lập thành công IAM Role Conditions để thắt chặt bảo mật truy cập theo IP và thời gian.
* Biết sử dụng Security Hub để theo dõi Compliance Score và phát hiện các rủi ro bảo mật.
* Nắm vững cách cấu hình Web ACL trên AWS WAF để bảo vệ ứng dụng web ở tầng ứng dụng (Layer 7).
