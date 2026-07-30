---
title: "Worklog Tuần 5"
date: 2026-06-14
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Tìm hiểu IAM Role cho ứng dụng (thay thế Access Key) và cách thiết lập, lập trình trong môi trường AWS Cloud9.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu workshop Cấp quyền cho ứng dụng truy cập dịch vụ AWS với IAM Role <br> - Tìm hiểu các phương pháp cấp quyền cho ứng dụng khi truy cập tài nguyên AWS <br> - Thực hành chuẩn bị môi trường và tài nguyên cần thiết cho workshop | 15/06/2026 | 15/06/2026 | <https://000048.awsstudygroup.com/> |
| 3   | - Tìm hiểu cơ chế xác thực bằng Access Key ID và Secret Access Key <br> - Phân tích các rủi ro bảo mật khi lưu trữ Access Key trực tiếp trong source code hoặc file cấu hình ứng dụng | 16/06/2026 | 16/06/2026 | <https://000048.awsstudygroup.com/> |
| 4   | - Thực hành tạo và cấu hình IAM Role cho Amazon EC2 <br> - Tìm hiểu cách EC2 Instance sử dụng IAM Role để truy cập các dịch vụ AWS mà không cần lưu trữ Access Key <br> - So sánh ưu điểm và nhược điểm giữa việc sử dụng Access Key và IAM Role <br> - Thực hiện dọn dẹp tài nguyên sau khi hoàn thành bài thực hành | 17/06/2026 | 17/06/2026 | <https://000048.awsstudygroup.com/> |
| 5   | - Nghiên cứu workshop Bắt đầu với AWS Cloud9 <br> - Tìm hiểu kiến trúc và vai trò của AWS Cloud9 trong quá trình phát triển ứng dụng trên nền tảng AWS <br> - Thực hành tạo môi trường phát triển (Cloud9 Environment) trên AWS | 18/06/2026 | 18/06/2026 | <https://000049.awsstudygroup.com/> |
| 6   | - Khám phá giao diện và các tính năng cơ bản của AWS Cloud9 IDE <br> - Thực hành sử dụng trình soạn thảo mã nguồn tích hợp trên Cloud9 <br> - Tìm hiểu hệ thống Terminal tích hợp và cách thực thi lệnh trực tiếp trên Cloud9 <br> - Thực hành sử dụng AWS CLI trong môi trường Cloud9 để tương tác với các dịch vụ AWS <br> - Nghiên cứu cơ chế tích hợp IAM Role và thông tin xác thực AWS trong Cloud9 <br> - Thực hiện dọn dẹp tài nguyên Cloud9 sau khi hoàn thành bài thực hành | 19/06/2026 | 19/06/2026 | <https://000049.awsstudygroup.com/> |

### Kết quả đạt được tuần 5:

* Hiểu nguyên lý hoạt động của IAM Role và cơ chế cấp quyền tạm thời (temporary credentials).
* Nắm được lý do AWS khuyến nghị sử dụng IAM Role thay vì Access Key cho ứng dụng chạy trên EC2.
* Hiểu được mối quan hệ giữa IAM Role, Policy và EC2 Instance Profile.
* Hiểu được AWS Cloud9 là môi trường phát triển tích hợp (IDE) chạy trực tiếp trên nền web.
* Nắm được quy trình tạo và quản lý Cloud9 Environment, IDE, Terminal và AWS CLI.
