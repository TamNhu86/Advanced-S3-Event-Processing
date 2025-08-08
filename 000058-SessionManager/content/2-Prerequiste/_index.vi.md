---
title : "Tổng quan kiến trúc"
date : 2025-06-27
weight : 2 
chapter : false
pre : " <b> 2. </b> "
---

{{% notice info %}}
Tài khoản AWS có quyền sử dụng S3, Lambda, Step Functions, IAM.
Hiểu cơ bản về AWS Lambda và Amazon S3.
Biết cách tạo role, policy và dùng AWS Console hoặc AWS CLI.
{{% /notice %}}

Hệ thống xử lý sự kiện nâng cao được thiết kế theo kiến trúc event-driven, sử dụng các thành phần không máy chủ (serverless) giúp mở rộng linh hoạt và tối ưu chi phí.

![S3](/images/2.prerequisite/2.Tongquankientruc.png)

### Luồng xử lý sự kiện từng bước:

1. Upload file vào S3:

- Người dùng hoặc hệ thống khác tải tệp (ảnh, CSV, JSON, log,...) vào một S3 bucket.

2. S3 phát sinh sự kiện:

- S3 kích hoạt sự kiện `s3:ObjectCreated:*` và gửi thông tin file qua SNS hoặc trực tiếp đến Lambda.

3. Lambda đầu tiên (preprocessing):

- Xử lý metadata, kiểm tra định dạng, lọc file lỗi, trích xuất thông tin cơ bản.

- Nếu hợp lệ → tiếp tục xử lý.

- Nếu không hợp lệ → ghi log lỗi và dừng.

4. Step Function orchestration:

- Step Functions điều phối toàn bộ quy trình

5. CloudWatch giám sát:

- Từng Lambda sẽ ghi log vào CloudWatch Logs.

- Step Functions có thể được theo dõi theo execution status.

6. Thông báo kết quả:

- Kết quả thành công hoặc lỗi sẽ được gửi đến người dùng qua SNS, Email, hoặc lưu log.
  
