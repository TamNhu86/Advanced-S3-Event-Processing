---
title: "Giới thiệu"
date:  2025-06-27
weight: 1 
chapter: false
pre : " <b> 1. </b> "
--- 

**Giới thiệu** 

Trong các hệ thống hiện đại, việc xử lý dữ liệu theo hướng sự kiện là phương pháp phổ biến để xây dựng các pipeline linh hoạt, tiết kiệm chi phí và dễ mở rộng. Workshop này hướng dẫn bạn cách xây dựng một hệ thống xử lý sự kiện phức tạp bắt nguồn từ Amazon S3, điều phối bởi AWS Step Functions và xử lý bởi AWS Lambda.

Bạn sẽ học cách tích hợp nhiều dịch vụ AWS để tạo thành một quy trình xử lý tự động hóa không máy chủ (serverless), có khả năng kiểm soát lỗi, retry và theo dõi trạng thái của toàn bộ luồng công việc.


**Mục tiêu** 

Sau khi hoàn thành workshop, bạn sẽ có thể:

- Thiết lập trigger từ Amazon S3 để khởi tạo quy trình xử lý khi có file được upload.
- Xây dựng chuỗi Lambda functions để xử lý dữ liệu.
- Thiết kế workflow với AWS Step Functions: tuần tự, song song, điều kiện và xử lý lỗi.
- Áp dụng các kỹ thuật xử lý lỗi: Retry, Catch, Dead Letter Queue.
- Giám sát toàn bộ hệ thống với CloudWatch Logs và Metrics.

**Nội dung thực hành** 

- Tạo S3 bucket và cấu hình sự kiện khi upload file.
- Viết Lambda function để xử lý tệp (ví dụ: phân tích metadata, gửi SNS).
- Tạo Step Function để điều phối nhiều Lambda thành một workflow.
- Cấu hình retry logic, xử lý ngoại lệ và gửi lỗi sang SNS/SQS.
- Kiểm tra, giám sát bằng CloudWatch và xác thực kết quả qua log và trạng thái Step Function.

**Kết quả đạt được** 


- Hoàn thành một hệ thống xử lý sự kiện tự động từ đầu vào S3.
- Hiểu cách hoạt động của kiến trúc event-driven trong môi trường AWS.
- Làm quen với mô hình serverless và các kỹ thuật quản lý lỗi thực tế.
- Ứng dụng được kiến thức vào các bài toán thực tế như: xử lý log, resize ảnh, phân tích dữ liệu đầu vào