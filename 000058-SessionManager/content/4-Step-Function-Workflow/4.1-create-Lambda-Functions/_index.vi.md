---
title : "Tạo thêm Lambda Functions (Xử lý chính và lưu kết quả)"
date :  "2025-06-27" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

#### Tạo Lambda xử lý nội dung (processFileFunction)

- Truy cập Lambda Console

- Nhấn Create function

- Điền thông tin:

    + Function name: `processFileFunction`

    + Runtime: Python 3.12

    + Execution role: Use existing role → chọn LambdaEventProcessingRole
  
![S3](/images/4-Step-Function-Workflow/4.1.png)

- Nhấn Create function

Trong mục Code, dán:
```python
def lambda_handler(event, context):
    print("Processing file content...")
    return {
        "status": "processed",
        "filename": event.get("filename", "unknown")
    }
```

![S3](/images/4-Step-Function-Workflow/4.2.png)

- Nhấn Deploy

#### Tạo Lambda lưu kết quả (storeResultFunction)
   
- Tiếp tục tạo function mới:
  
  ![S3](/images/4-Step-Function-Workflow/4.3.png)

- Function name: `storeResultFunction`

- Runtime: Python 3.12

- Execution role: LambdaEventProcessingRole

- Code mẫu:

```python
def lambda_handler(event, context):
    print("Storing result...")
    print("Input from previous step:", event)
    return {
        "status": "stored",
        "original": event
    }
```

  ![S3](/images/4-Step-Function-Workflow/4.4.png)

- Nhấn Deploy

