---
title: "Worklog Tuần 6"
date: 2026-06-21
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Tìm hiểu dịch vụ S3 (Static Website, CloudFront), RDS Database, Amazon Lightsail và triển khai ứng dụng với Load Balancer và Auto Scaling Group.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu dịch vụ Amazon S3, quy trình tạo và cấu hình S3 Bucket <br> - Thực hành bật tính năng Static Website Hosting trên S3, kiểm tra hoạt động <br> - Tìm hiểu cơ chế Block Public Access và cấu hình quyền truy cập công khai cho Object | 22/06/2026 | 22/06/2026 | <https://000057.awsstudygroup.com/> |
| 3   | - Tìm hiểu cách sử dụng Amazon CloudFront để tăng tốc website <br> - Nghiên cứu Bucket Versioning, sao chép dữ liệu S3 giữa các Region (Cross-Region Replication) <br> - Dọn dẹp tài nguyên S3 | 23/06/2026 | 23/06/2026 | <https://000057.awsstudygroup.com/> |
| 4   | - Nghiên cứu tổng quan về dịch vụ Amazon RDS <br> - Thực hành tạo EC2 Instance và RDS Database Instance <br> - Kết nối EC2 với RDS thông qua Security Group & Endpoint <br> - Triển khai ứng dụng sử dụng RDS, thực hành sao lưu (Backup) và khôi phục (Restore) <br> - Dọn dẹp tài nguyên RDS | 24/06/2026 | 24/06/2026 | <https://000005.awsstudygroup.com/> |
| 5   | - Nghiên cứu Amazon Lightsail và tối ưu chi phí trên AWS <br> - Triển khai Lightsail Database và các ứng dụng WordPress, PrestaShop, Akaunting trên Lightsail <br> - Thực hành tạo Snapshot để sao lưu, nâng cấp tài nguyên (Scale Up), tạo Monitoring & Alert để giám sát tài nguyên <br> - Dọn dẹp tài nguyên Lightsail | 25/06/2026 | 25/06/2026 | <https://000045.awsstudygroup.com/> |
| 6   | - Nghiên cứu triển khai ứng dụng FCJ Management với Auto Scaling Group (ASG) <br> - Tạo EC2 Launch Template, cấu hình Application Load Balancer (ALB) và tạo ASG <br> - Kiểm thử các kịch bản Auto Scaling bằng cách mô phỏng tải hệ thống <br> - Dọn dẹp tài nguyên ASG | 26/06/2026 | 26/06/2026 | <https://000006.awsstudygroup.com/> |

### Kết quả đạt được tuần 6:

* Hiểu được kiến trúc lưu trữ đối tượng của Amazon S3, quy trình deploy website tĩnh và tích hợp CloudFront.
* Nắm được cách tạo và kết nối RDS Database với ứng dụng chạy trên EC2.
* Hiểu lợi ích của Amazon Lightsail, quy trình deploy app và cấu hình Snapshot.
* Nắm vững vai trò và sự liên kết giữa Launch Template, ALB và ASG trong việc tự động mở rộng hệ thống.
