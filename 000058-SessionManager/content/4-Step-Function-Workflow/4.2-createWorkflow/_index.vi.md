---
title : "Tạo Step Functions Workflow"
date :  "2025-06-27" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

1. Truy cập Step Functions
   
-  Truy cập giao diện Step Functions Console
  
- Nhấn Create state machine

- Nhập tên `FileProcessingWorkflow`

![S3](/images/4-Step-Function-Workflow/4.5.png)

- Chọn Author with code snippets

- Nhập cấu hình JSON Workflow:
  
  + Ở tab Definition, dán đoạn mã sau (nhớ sửa id của bạn):
```
 {
  "StartAt": "Process File",
  "States": {
    "Process File": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:<account-id>:function:processFileFunction",
      "Next": "Store Result",
      "Retry": [
        {
          "ErrorEquals": ["States.ALL"],
          "IntervalSeconds": 2,
          "MaxAttempts": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "Fail Handler"
        }
      ]
    },
    "Store Result": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:<account-id>:function:storeResultFunction",
      "End": true
    },
    "Fail Handler": {
      "Type": "Fail",
      "Error": "WorkflowFailed",
      "Cause": "Lambda function failed"
    }
  }
}
```

![S3](/images/4-Step-Function-Workflow/4.6.png)


📌 Giải thích:

- Retry: tự động chạy lại nếu Lambda lỗi

- Catch: chuyển hướng đến bước Fail Handler nếu tất cả retry thất bại

2. Tạo workflow

- Nhấn Next

- Kiểm tra lại tên, role, quyền

- Nhấn Create state machine

![S3](/images/4-Step-Function-Workflow/4.7.png)

![S3](/images/4-Step-Function-Workflow/4.8.png)

