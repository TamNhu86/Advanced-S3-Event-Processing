---
title : "Test cảnh báo"
date :  "2025-06-27" 
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---
#### Test 1: Kích hoạt cảnh báo khi Lambda lỗi nhiều lần

🎯 Mục tiêu:
Kích hoạt CloudWatch Alarm đã cấu hình cho processFileFunction (hoặc Lambda nào bạn đã chọn), bằng cách cố tình làm Lambda thất bại nhiều lần trong 5 phút.

- Bước 1: Sửa Lambda để gây lỗi cố tình

![S3](/images/5.fwd/test01.png)
  
  + Vào AWS Lambda Console

  + Mở hàm Lambda (processFileFunction)

  + Chọn tab Code

  + Thay code như sau (Node.js hoặc Python) để luôn lỗi:

Với Python:
```
def lambda_handler(event, context):
    raise Exception("Forced test error")
```

  +  Nhấn Deploy để áp dụng thay đổi

- Bước 2: Gọi Lambda liên tục để tạo lỗi

![S3](/images/5.fwd/test02.png)

  + Tại Lambda Console → chọn tab Test

  + Tạo event test mẫu:
```
{
  "test": true
}
```

  + Nhấn Test từ 3–5 lần liên tục trong vòng 1–2 phút

📌 Mục tiêu: Có nhiều lần gọi thất bại → tổng số Errors > 1 trong 5 phút

![S3](/images/5.fwd/test03.png)

![S3](/images/5.fwd/test04.png)

-  Bước 3: Theo dõi cảnh báo
  
   + Vào CloudWatch → Alarms
  
![S3](/images/5.fwd/test05.png)

   + Xem alarm LambdaErrorAlarm có chuyển từ trạng thái OK → ALARM không (mất vài phút)

   + Kiểm tra email nhận cảnh báo nếu gắn SNS Topic

![S3](/images/5.fwd/thongbaotest01.png)

#### Test 2: Kích hoạt cảnh báo khi Step Function thất bại

- Bước 1: Vào Step Functions Console

  + Mở FileProcessingWorkflow.

  + Nhấn “Start execution”

![S3](/images/5.fwd/testreal.png)

Nhập Input như sau (tuỳ bạn code thế nào, nhưng hãy dùng input khiến Lambda gọi lỗi):
```
{
  "simulateError": true
}
```

Hoặc nếu bạn không xử lý input: chỉ cần để Lambda trong step raise Exception(...) mặc định là đủ.

Chạy workflow → để nó lỗi

![S3](/images/5.fwd/fail.png)

Kiểm tra Execution status: phải là Failed

- Bước 2: Sau khi chạy lỗi:
  
  + Chờ khoảng 1–5 phút

  + CloudWatch sẽ cập nhật metric ExecutionsFailed > 
  
![S3](/images/5.fwd/erroalarm.png)

- Bước 3: Kiểm tra lại alarm:
  
  + Vào lại CloudWatch → Alarms

  + Nếu thấy StepFunctionFailureAlarm chuyển từ ❔ Insufficient data sang 🔴 In alarm là bạn test thành công 

![S3](/images/5.fwd/erroalarm2.png)

  + Kiểm tra email (nếu bạn đã gắn SNS topic vào alarm đó và xác nhận email):

Bạn sẽ nhận được cảnh báo lỗi Step Function.

  + Kiểm tra email (nếu bạn đã gắn SNS topic vào alarm đó và xác nhận email):

![S3](/images/5.fwd/tbreal.png)
