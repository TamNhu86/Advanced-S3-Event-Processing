---
title : "Kiểm tra log từ Lambda và Step Functions"
date :  "2025-06-27" 
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---
#### Logs của Lambda Function

- Truy cập CloudWatch Console

- Chọn Logs → Log groups

- Tìm theo tên hàm: /aws/lambda/s3PreprocessFunction, processFileFunction, storeResultFunction

![S3](/images/3-Accessibilitytoinstances/3.3.10output.png)

- Chọn group → click log stream để xem chi tiết từng lần invoke

#### Logs của Step Function

- Truy cập lại Step Functions Console

- Chọn state machine FileProcessingWorkflow

- Nhấn vào execution bất kỳ → tab Execution events sẽ hiển thị chi tiết:

- Input/Output từng bước

![S3](/images/5.fwd/5.3.png)

![S3](/images/5.fwd/5.4.png)

- Trạng thái succeed/fail:

![S3](/images/5.fwd/5.3.1.png)

- Error message nếu có lỗi

![S3](/images/5.fwd/5.erro.png)