---
title : "Tạo IAM Role cho Lambda"
date :  "2025-06-27" 
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
--- 


**Bước 1:** Mở trang tạo Role

- Vào IAM Roles

- Nhấn nút “Create role” (góc phải trên)

**Bước 2:** Chọn Trusted Entity (Lambda service)

- Ở mục Trusted entity type, chọn "AWS service"

![S3](/images/3-Accessibilitytoinstances/3.2.1.png)

- Trong phần “Use case”, chọn "Lambda"

- Nhấn Next

**Bước 3:** Gán quyền (Attach policies)

- Tìm và tick chọn 3 policies sau:

![S3](/images/3-Accessibilitytoinstances/3.2.2.png)

- Policy name	Mục đích: 

  + AmazonS3ReadOnlyAccess: 	Cho phép Lambda đọc object từ S3

  + CloudWatchLogsFullAccess: 	Ghi log vào CloudWatch

  + AWSStepFunctionsFullAccess: 	Cho phép Lambda gọi Step Functions hoặc Step Functions invoke Lambda

- Nhấn Next

**Bước 4** Gán tên và mô tả
- Role name: LambdaEventProcessingRole

- Description (tuỳ chọn): Role for Lambda functions to access S3, Step Functions and CloudWatch

- Nhấn Create role

**Bước 5:** Kiểm tra Role đã tạo

- Trong danh sách IAM Roles, tìm LambdaEventProcessingRole

- Click vào tên role để mở chi tiết

- Xác nhận:

![S3](/images/3-Accessibilitytoinstances/3.2.4.png)

- Trusted entity: lambda.amazonaws.com

- Policies attached: gồm đủ 3 quyền đã chọn

✅ Kết quả

- Bạn đã tạo xong IAM Role tên LambdaEventProcessingRole cho các Lambda functions dùng trong workflow xử lý sự kiện. Role này sẽ được gán cho các hàm như:

  + s3PreprocessFunction

  + processFileFunction

  + storeResultFunction