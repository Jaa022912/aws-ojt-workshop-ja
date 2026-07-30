---
title: "Blog 1"
date: 2024-06-05
weight: 1
chapter: false
pre: "<b>3.1.</b>"
---

# Tìm Hiểu AI Traffic Analysis Dashboards Trong AWS WAF

## Giới thiệu

Sự phát triển nhanh chóng của các mô hình AI như **ChatGPT**, **Claude** hay **Perplexity** không chỉ thay đổi cách con người tìm kiếm thông tin mà còn tạo ra một loại lưu lượng truy cập mới đến các website: **AI Traffic**. Điều này đặt ra những thách thức mới trong việc giám sát, tối ưu tài nguyên và bảo mật hệ thống.

Trong quá trình tìm hiểu về các dịch vụ bảo mật trên AWS, mình có đọc bài viết **Introducing AI Traffic Analysis Dashboards for AWS WAF** được AWS Security Blog giới thiệu. Điều khiến mình quan tâm không chỉ là giao diện dashboard mà còn là cách AWS nhìn nhận AI traffic như một loại lưu lượng riêng cần được theo dõi và phân tích.

Trong bài viết này, mình sẽ chia sẻ những nội dung mình tìm hiểu được về **AI Traffic Analysis Dashboards** trong AWS WAF cũng như những điều rút ra sau khi đọc tài liệu chính thức từ AWS.

---

## AI Traffic Analysis Dashboards là gì?

Trong quá trình tìm hiểu về các dịch vụ bảo mật trên AWS, mình nhận thấy AWS vừa giới thiệu một tính năng mới của **AWS WAF** có tên là **AI Traffic Analysis Dashboards**.

Điều làm mình chú ý không phải là giao diện dashboard hay các biểu đồ thống kê, mà là vấn đề AWS đang cố gắng giải quyết.

Trước đây khi học về bảo mật web, mình thường nghĩ lưu lượng truy cập vào website chủ yếu đến từ người dùng hoặc các bot tự động. Các giải pháp như AWS WAF thường được sử dụng để phát hiện và ngăn chặn các request bất thường nhằm bảo vệ ứng dụng.

Tuy nhiên, với sự phát triển của các hệ thống AI như **ChatGPT**, **Claude** hay **Perplexity**, ngày càng có nhiều AI crawler truy cập website để thu thập dữ liệu hoặc hỗ trợ việc tìm kiếm và trả lời câu hỏi. Những request này không phải là tấn công nhưng vẫn tiêu tốn tài nguyên hệ thống giống như bất kỳ request nào khác.

Đó cũng chính là lý do AWS phát triển **AI Traffic Analysis Dashboards**.

---

## AWS WAF đang theo dõi điều gì?

Theo bài viết của AWS, dashboard mới được xây dựng nhằm giúp người quản trị biết được những hệ thống AI nào đang truy cập vào ứng dụng của mình.

Ví dụ:

- GPTBot của OpenAI
- ClaudeBot của Anthropic
- PerplexityBot
- Googlebot
- Các AI crawler khác

Thay vì chỉ hiển thị tổng số request, dashboard còn cung cấp:

- Bot AI nào đang hoạt động nhiều nhất.
- Số lượng request của từng bot.
- Xu hướng AI traffic theo thời gian.
- Các URL được AI truy cập nhiều nhất.

![AI Traffic Analysis Dashboard](ai-traffic-dashboard.jpg)

*Hình 1. AI Traffic Analysis Dashboard trong AWS WAF hiển thị Top Crawlers, Bot Traffic Volume, Top Paths và Most Accessed Paths.*

Quan sát dashboard có thể thấy AWS cung cấp khá nhiều thông tin hữu ích:

- **Top Crawlers:** Thống kê các AI crawler phổ biến như GPTBot, ClaudeBot, Googlebot...
- **Bot Traffic Volume:** Biểu đồ thể hiện lưu lượng truy cập của AI theo thời gian.
- **Top Paths:** Những URL được AI truy cập nhiều nhất.
- **Most Accessed Paths:** Mối liên hệ giữa từng AI bot với các đường dẫn mà chúng thường truy cập.

Khi đọc đến đây mình nhận ra rằng việc theo dõi AI traffic cũng quan trọng không kém việc theo dõi người dùng thông thường. Nếu một website có lượng AI crawler lớn, chi phí hạ tầng hoàn toàn có thể tăng lên đáng kể mà người quản trị không nhận ra nguyên nhân.

---

## Nhận diện bot không đơn giản như mình nghĩ

Ban đầu mình nghĩ việc xác định bot chủ yếu dựa vào **User-Agent**.

Ví dụ:

```text
User-Agent: GPTBot
```

Tuy nhiên AWS cho biết hệ thống của họ không chỉ dựa vào thông tin này vì **User-Agent hoàn toàn có thể bị giả mạo**.

Để tăng độ chính xác, AWS WAF Bot Control còn sử dụng thêm nhiều cơ chế xác thực nhằm nhận diện bot đáng tin cậy thay vì chỉ dựa trên chuỗi User-Agent.

Điều này giúp mình hiểu rằng trong thực tế, không phải request nào tự nhận là GPTBot cũng thực sự đến từ GPTBot.

---

## AI đang truy cập những nội dung nào?

Một tính năng khác mà mình thấy khá hữu ích là khả năng thống kê những URL hoặc endpoint được AI truy cập nhiều nhất.

Ví dụ:

- Trang blog
- Tài liệu kỹ thuật
- API
- Trang sản phẩm

Thông tin này giúp đội ngũ vận hành biết khu vực nào đang nhận nhiều AI traffic nhất.

Nếu một API nội bộ nhận quá nhiều request từ crawler, doanh nghiệp có thể:

- Giới hạn tốc độ truy cập (Rate Limiting).
- Tăng cường cơ chế Cache.
- Điều chỉnh chính sách Bot Control phù hợp.

Nhờ đó hệ thống có thể giảm tải và tối ưu chi phí vận hành.

---

## Theo dõi sự thay đổi của AI Traffic

Dashboard còn hỗ trợ theo dõi dữ liệu theo thời gian.

Người quản trị có thể quan sát:

- AI traffic tăng hay giảm.
- Bot nào hoạt động nhiều nhất.
- Thời điểm xuất hiện các đợt truy cập bất thường.
- Xu hướng AI crawler theo từng khoảng thời gian.

Theo mình đây là tính năng khá hữu ích vì nó giúp phát hiện những thay đổi mà đôi khi rất khó nhận ra nếu chỉ xem log hoặc số lượng request tại một thời điểm.

---

## Điều mình học được

Sau khi đọc bài viết, điều mình thấy thú vị nhất là AWS đang xem **AI Traffic** như một loại lưu lượng riêng thay vì gộp chung với các bot truyền thống.

Trước đây khi học về bảo mật web, phần lớn nội dung chỉ tập trung vào người dùng và các cuộc tấn công.

Hiện nay, sự xuất hiện của **AI Agents** và **AI Crawlers** đã tạo ra một nhóm truy cập hoàn toàn mới. Chúng không mang mục đích tấn công nhưng vẫn ảnh hưởng đến tài nguyên, hiệu năng và chi phí vận hành của hệ thống.

Điều đó cũng đồng nghĩa với việc các công cụ bảo mật cần bổ sung khả năng quan sát và phân tích để doanh nghiệp hiểu rõ hơn những gì đang diễn ra trên ứng dụng của mình.

---

## Kết luận

AI Traffic Analysis Dashboards không phải là tính năng dùng để chặn AI hay ngăn cản các hệ thống AI truy cập website.

Mục đích chính của tính năng này là:

- Giúp doanh nghiệp quan sát AI traffic.
- Phân tích hành vi của các AI crawler.
- Theo dõi xu hướng truy cập theo thời gian.
- Hỗ trợ đưa ra các quyết định tối ưu hạ tầng và chính sách bảo mật.

Đối với mình, đây là một ví dụ khá thú vị về việc các dịch vụ Cloud phải liên tục thay đổi để thích nghi với sự phát triển của AI. Khi số lượng AI Agents ngày càng tăng, việc theo dõi và quản lý loại lưu lượng này có thể sẽ trở thành một phần quen thuộc trong công tác vận hành và bảo mật ứng dụng.

---

# Tài liệu tham khảo

## Bài viết gốc

**Introducing AI Traffic Analysis Dashboards for AWS WAF**

https://aws.amazon.com/blogs/security/introducing-ai-traffic-analysis-dashboards-for-aws-waf/

---

## AWS WAF Documentation

https://docs.aws.amazon.com/waf/

---

## AI Traffic Analysis Dashboards

https://docs.aws.amazon.com/waf/latest/developerguide/waf-bot-control-ai-traffic.html

## Bài viết liên quan

- **Facebook:** [AI Traffic Analysis Dashboards trong AWS WAF](https://www.facebook.com/groups/660548818043427/user/100038533741109/)
---

## Các dịch vụ liên quan

- AWS WAF
- AWS WAF Bot Control
- Amazon CloudWatch
- AWS Shield
- AWS Firewall Manager

---

# Nguồn tham khảo

1. AWS Security Blog. *Introducing AI Traffic Analysis Dashboards for AWS WAF*.
   https://aws.amazon.com/blogs/security/introducing-ai-traffic-analysis-dashboards-for-aws-waf/

2. AWS Documentation. *AWS WAF Developer Guide*.
   https://docs.aws.amazon.com/waf/

3. AWS Documentation. *AI Traffic Analysis Dashboards*.
   https://docs.aws.amazon.com/waf/latest/developerguide/waf-bot-control-ai-traffic.html