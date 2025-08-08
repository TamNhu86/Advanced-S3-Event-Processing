---
title : "Dọn dẹp tài nguyên"
date :  "2025-06-27" 
weight : 6 
chapter : false
pre : " <b> 6. </b> "
---

1. Xóa Step Function State Machine

![S3](/images/6.clean/delete1.png)

  - Truy cập Step Functions Console

  - Chọn FileProcessingWorkflow

  - Nhấn Actions → Delete state machine

  - Xác nhận xóa

2. Xóa các Lambda Functions

![S3](/images/6.clean/delete2.png)

   - Vào Lambda Console

   - Xóa lần lượt các function:

      + s3PreprocessFunction

      + processFileFunction

      + storeResultFunction

3. Xóa bucket S3 

  ![S3](/images/6.clean/emty.png)

  - Chọn bucket event-driven-demo-bucket 
  
  - Empty bucket
  
  - Xóa bucket S3

4. Xóa IAM Role nếu không dùng cho mục đích khác

  ![S3](/images/6.clean/deleterole.png)