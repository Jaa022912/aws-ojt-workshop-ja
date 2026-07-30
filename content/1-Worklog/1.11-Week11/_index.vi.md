---
title: "Worklog Tuần 11"
date: 2026-07-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Triển khai ứng dụng container hóa trên AWS bằng Docker, Docker Compose và Amazon ECR; Quản trị và mở rộng container tự động với Amazon ECS (Service Discovery, ALB); Tự động hóa quy trình với CI/CD Pipeline (GitHub Actions/GitLab CI) và giám sát logs/container.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2   | - Nghiên cứu triển khai ứng dụng Docker trên AWS <br> - Thực hành viết Dockerfile, chạy thử local, sau đó tạo RDS Database, EC2 Instance cài Docker và chạy ứng dụng container kết nối với RDS | 27/07/2026 | 27/07/2026 | <https://000015.awsstudygroup.com/vi/> |
| 3   | - Thực hành sử dụng Docker Compose để quản lý nhiều container <br> - Đẩy (Push) Docker Image lên Amazon Elastic Container Registry (ECR) để lưu trữ và quản lý phiên bản | 28/07/2026 | 28/07/2026 | <https://000015.awsstudygroup.com/vi/> |
| 4   | - Nghiên cứu Amazon Elastic Container Service (Amazon ECS) <br> - Khởi tạo ECS Cluster, cấu hình ECS Task Definition (Docker Image, CPU, Memory, Network) và triển khai ECS Service | 29/07/2026 | 29/07/2026 | <https://000016.awsstudygroup.com/vi/> |
| 5   | - Cấu hình Application Load Balancer (ALB) và AWS Cloud Map (Service Discovery) để định tuyến lưu lượng truy cập và tự động phát hiện dịch vụ trong ECS Cluster | 30/07/2026 | 30/07/2026 | <https://000016.awsstudygroup.com/vi/> |
| 6   | - Triển khai CI/CD Pipeline bằng GitHub Actions, GitLab CI/CD và AWS CodeBuild <br> - Tự động hóa build/push Docker Image lên ECR và deploy lên ECS <br> - Giám sát bằng CloudWatch Container Insights và FireLens Logging <br> - Dọn dẹp tài nguyên | 31/07/2026 | 31/07/2026 | <https://000017.awsstudygroup.com/vi/> |

### Kết quả đạt được tuần 11:

* Nắm vững quy trình build và deploy ứng dụng container hóa bằng Docker, Docker Compose và quản lý trên Amazon ECR.
* Hiểu rõ vai trò của ECS Cluster, Task Definition, ECS Service, ALB và Service Discovery.
* Thiết lập thành công CI/CD pipeline để tự động hóa việc phát triển và triển khai container.
* Biết sử dụng Container Insights và FireLens để quản lý, giám sát log và hiệu năng container trên AWS.
