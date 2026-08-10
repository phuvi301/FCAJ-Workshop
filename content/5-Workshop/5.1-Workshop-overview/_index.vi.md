---
title: "Giới thiệu & Tổng quan"
date: 2026-07-30
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Giới Thiệu Dự Án CodExecute

**CodExecute** là giải pháp nền tảng chấm bài trực tuyến (Online Judge Platform) và mạng xã hội lập trình viên hiện đại, cho phép biên dịch, thực thi và đánh giá kết quả mã nguồn của người dùng (C++, Java, Python, JavaScript) theo thời gian thực.

Dự án được thiết kế chuẩn theo mô hình **Pure Serverless Cloud-Native AWS**, tập trung giải quyết 3 bài toán lớn của các hệ thống chấm bài truyền thống:
1. **Chống RCE (Remote Code Execution) & Đảm bảo an toàn hệ thống:** Cách ly hoàn toàn mã nguồn chưa kiểm duyệt của người dùng trong môi trường **AWS Lambda Worker Sandbox** không có quyền root và bị chặn truy cập mạng ngoài.
2. **Xử lý dồn dập bài nộp (Traffic Spikes):** Sử dụng hàng chờ **Amazon SQS** làm vùng đệm điều tiết lưu lượng nộp bài, giúp hệ thống không bị crash hay nghẽn cổ chai.
3. **Tối ưu chi phí vận hành (Pay-As-You-Go):** Tự động thu phóng tài nguyên từ 0 (Scale-to-Zero) khi không có lượt nộp bài, cắt giảm đến 75% chi phí máy chủ nhàn rỗi.

---

### Mô Hình Kiến Trúc Dự Án

Hệ thống CodExecute vận hành dựa trên sự phối hợp của 8 dịch vụ AWS cốt lõi:

* **Amazon CloudFront & Amazon S3:** Phân phối giao diện React Frontend tĩnh toàn cầu với độ trễ tối thiểu và lưu trữ bộ dữ liệu Testcases (Input/Output).
* **Amazon API Gateway & AWS Lambda (API Handler):** Tiếp nhận các HTTP RESTful API request và xử lý logic ứng dụng.
* **Amazon SQS (Submissions Queue):** Lưu trữ hàng chờ bài nộp bất đồng bộ để điều tiết lưu lượng cho Worker.
* **AWS Lambda (Worker Sandbox Runner):** Đọc job từ SQS, tải Testcase từ S3, thực thi và chấm điểm mã nguồn trong môi trường Sandbox cách ly.
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL tốc độ cực cao lưu trữ toàn bộ dữ liệu người dùng, bài tập, lượt nộp và mạng xã hội.
* **Amazon CloudWatch & AWS IAM:** Giám sát nhật ký (Logs), thiết lập cảnh báo (Alarms) và phân quyền bảo mật tối thiểu (Least Privilege Access).

<div align="center">

<img src="/images/2-Proposal/architect-codexecute.drawio.png" alt="Sơ đồ kiến trúc CodExecute" style="width: 70%; max-width: 900px; border-radius: 6px;">

<p style="font-size: 1.15rem; font-weight: 600; margin-top: 8px;">
<i>Sơ đồ tổng quan kiến trúc hệ thống CodExecute trên AWS Serverless</i>
</p>

<img src="/images/5-Workshop/5.1-Workshop-overview/project_overview.png" alt="Trang giao diện Web của CodExecute" style="width: 80%; max-width: 1100px; border-radius: 6px;">
<p style="font-size: 1.15rem; font-weight: 600; margin-top: 8px;">
<i>Trang giao diện Web của CodExecute</i></br>
<i>Link demo: </i><a target="blank" href="https://drive.google.com/file/d/15AeqXtTXdVslTlJy3HmrP7IP6lOOiFaS/view?usp=sharing">Bấm vào đây</a>
</p>

</div>
