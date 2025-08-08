---
title : "Tạo cảnh báo với CloudWatch Alarm"
date :  "2025-06-27" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Cảnh báo khi Lambda lỗi nhiều lần

- Vào lại CloudWatch Console

- Trong menu trái, chọn Alarms → All alarms → Create alarm

- Bấm Select metric

![S3](/images/5.fwd/createalarms.png)

- Điều hướng:

- Browse → chọn Lambda

→ By Function Name

![S3](/images/5.fwd/unctionname.png)

→ chọn function processFileFunction

- Chọn metric Errors → Select metric

![S3](/images/5.fwd/erro.png)

- Thiết lập điều kiện:

    + Statistic: Sum

    + Period: 5 minutes

    + Threshold type: Static

    + Define threshold: Greater than 1
![S3](/images/5.fwd/5.02.01.png)

- Nhấn Next

- Thiết lập hành động:

- Notification:

- Chọn hoặc tạo SNS Topic (nếu chưa có, chọn “Create new topic”)

![S3](/images/5.fwd/5.02.02.png)

- Nhập email nhận cảnh báo

- Sau khi tạo, nhớ xác nhận email gửi từ AWS

![S3](/images/5.fwd/5.02.03.png)

- Đặt tên alarm: `LambdaErrorAlarm`

![S3](/images/5.fwd/5.02.04.png)

- Nhấn Create alarm

#### Cảnh báo khi Step Function thất bại

- Bước 1: Truy cập Metrics của Step Functions
Vào AWS Console: CloudWatch

  + Vào Metrics → chọn Browse
  
![S3](/images/5.fwd/5.03.01.png)

  + Chọn nhóm dịch vụ States → tiếp tục chọn Execution Metrics

![S3](/images/5.fwd/5.03.02.png)

  + Tìm đến metric: ExecutionsFailed của state machine FileProcessingWorkflow

- Bước 2: Tạo Alarm
  
![S3](/images/5.fwd/5.03.03.png)

  + Tick vào dòng ExecutionsFailed

  + Nhấn nút Create alarm (góc phải trên)

- Bước 3: Cấu hình điều kiện cảnh báo
  
![S3](/images/5.fwd/5.03.04.png)

  + Metric: ExecutionsFailed

  + Statistic: Sum

  + Period: 5 minutes

  + Condition: Greater than 0

  + Threshold type: Static

- Bước 4: Gán hành động cảnh báo

![S3](/images/5.fwd/5.03.05.png)
  
  + Chọn In alarm

  + Chọn SNS Topic đã tạo trước đó để nhận email

  + Nếu chưa có, nhấn Create new topic, nhập email và xác nhận email từ AWS

- Bước 5: Đặt tên và tạo alarm
  
![S3](/images/5.fwd/5.03.06.png)

  + Alarm name: StepFunctionFailureAlarm

  + Nhấn Next, rồi Create alarm

![S3](/images/5.fwd/5.03.07.png)

✅ Kết quả: Sau khi tạo xong, hệ thống sẽ theo dõi và gửi cảnh báo nếu Step Function thất bại trong khoảng thời gian 5 phút.

✅ Kết quả sau khi cấu hình
CloudWatch ghi log cho tất cả các hàm Lambda và Step Function

Cảnh báo sẽ gửi email nếu hệ thống bị lỗi

Giúp bạn dễ dàng giám sát, nhanh chóng phản ứng nếu workflow hỏng