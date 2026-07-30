---
title: "Worklog Tuần 8"
date: 2026-07-05
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

* Thiết lập Hybrid DNS và AWS CLI; Tìm hiểu VM Import/Export, Database Migration (SCT/DMS) và tối ưu chi phí EC2 bằng Lambda.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu workshop Thiết lập DNS lai với Amazon Route 53 Resolver <br> - Tìm hiểu tổng quan về Amazon Route 53 và vai trò của DNS trong hạ tầng AWS <br> - Chuẩn bị môi trường, kết nối qua RDGW và triển khai Microsoft Active Directory | 06/07/2026 | 06/07/2026 | <https://000010.awsstudygroup.com/> |
| 3   | - Cấu hình DNS Hybrid, bao gồm Route 53 Resolver Inbound và Outbound Endpoints, Resolver Rules <br> - Kiểm tra khả năng phân giải tên miền giữa AWS và on-premises <br> - Dọn dẹp tài nguyên Route 53 Resolver | 07/07/2026 | 07/07/2026 | <https://000010.awsstudygroup.com/> |
| 4   | - Nghiên cứu tổng quan về AWS CLI <br> - Cài đặt và cấu hình AWS CLI bằng lệnh `aws configure`, thiết lập Access Key, Secret Key, Region và Output <br> - Tìm hiểu cơ chế hoạt động của AWS CLI Profile để quản lý nhiều tài khoản <br> - Nghiên cứu dịch vụ AWS VM Import/Export và quy trình di chuyển máy ảo lên AWS | 08/07/2026 | 08/07/2026 | <https://000011.awsstudygroup.com/> |
| 5   | - Thực hành quản lý và tương tác với các tài nguyên AWS qua CLI (VPC, EC2, S3, SNS, IAM) <br> - Nghiên cứu quy trình Schema Conversion và Database Migration trên AWS <br> - Tìm hiểu vai trò của AWS Schema Conversion Tool (AWS SCT) và AWS DMS | 09/07/2026 | 09/07/2026 | <https://000011.awsstudygroup.com/> |
| 6   | - Tìm hiểu các lỗi thường gặp khi sử dụng AWS CLI và cách khắc phục <br> - Thực hành import máy ảo từ on-premises lên Amazon EC2. <br> - Nghiên cứu giải pháp tối ưu chi phí EC2 bằng AWS Lambda (tự động bật/tắt EC2 Instance theo Tag) <br> - Dọn dẹp tài nguyên bài lab | 10/07/2026 | 10/07/2026 | <https://000011.awsstudygroup.com/> |

### Kết quả đạt được tuần 8:

* Hiểu được vai trò của Route 53, Resolver Inbound/Outbound và Rules trong môi trường Hybrid Cloud.
* Nắm vững quy trình cài đặt, cấu hình AWS CLI Profile và cách quản lý tài nguyên AWS qua CLI.
* Hiểu cơ chế hoạt động của VM Import/Export để di chuyển máy ảo từ on-premises lên EC2.
* Nắm được sự khác biệt giữa Schema Conversion (SCT) và Data Migration (DMS).
* Hiểu cách sử dụng Lambda để tự động hóa các tác vụ quản trị và tối ưu chi phí vận hành EC2.
