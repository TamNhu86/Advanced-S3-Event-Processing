---
title : "Thiết lập Trigger từ S3 đến Lambda"
date :  "2025-06-27" 
weight : 5
chapter : false
pre : " <b> 3.4 </b> "
--- 
**Bước 1:**

- Tìm và nhấn vào tên bucket bạn đã tạo (ví dụ: event-driven-demo-bucket)
  
    + Tạo folder uploads và up load 1 file .jpg
  
    ![S3](/images/3-Accessibilitytoinstances/3.3.5folderupload.png)


    ![S3](/images/3-Accessibilitytoinstances/3.3.6upload.png)
  
- Mở phần cấu hình sự kiện
  
    + Trong giao diện bucket → chọn tab Properties

    + Cuộn xuống phần Event notifications

    + Nhấn nút “Create event notification”

- Cấu hình event trigger
  
    + Nhập tên tùy ý, ví dụ: `TriggerLambdaOnUpload`
  
     ![S3](/images/3-Accessibilitytoinstances/3.3.7createeventnotification.png)

    + Tick vào: ✅ All object create events (hoặc chỉ PUT nếu bạn chỉ muốn khi upload file)

    ![S3](/images/3-Accessibilitytoinstances/3.3.8event.png)

- Prefix và suffix (tùy chọn):

    + Prefix (tùy chọn): Ví dụ uploads/ nếu bạn chỉ muốn theo dõi thư mục cụ thể

    + Suffix (tùy chọn): .csv nếu bạn chỉ muốn xử lý file CSV

    (Ở ví dụ này ta dùng Suffix)

- Destination:
  
    ![S3](/images/3-Accessibilitytoinstances/3.3.9.png)

    + Chọn: Lambda function

    + Tên hàm: s3PreprocessFunction (nó sẽ hiện dropdown để bạn chọn)

- Lưu cấu hình: Nhấn nút Save changes


✅ Kết quả

- Mỗi khi bạn upload một file vào bucket, Lambda s3PreprocessFunction sẽ tự động được kích hoạt.

- Bạn có thể vào CloudWatch Logs để xem log ghi lại từ Lambda sau mỗi lần upload.

🎯 Kiểm tra lại

- Thử upload một file .txt hoặc .csv vào bucket qua giao diện

- Mở AWS CloudWatch Logs → tìm log group /aws/lambda/s3PreprocessFunction

- Tìm log group tên: /aws/lambda/s3PreprocessFunction

- Xem dòng log mới nhất → bạn sẽ thấy output như sau:
  
  ![S3](/images/3-Accessibilitytoinstances/3.3.10output.png)