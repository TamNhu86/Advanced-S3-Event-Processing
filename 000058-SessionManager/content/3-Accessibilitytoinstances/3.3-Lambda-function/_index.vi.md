---
title : "Tạo Lambda Function: Tiền xử lý"
date :  "2025-06-27" 
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
--- 

**Bước 1:** Truy cập Lambda Console

- Nhấn “Create function”

- Cấu hình Lambda Function

![S3](/images/3-Accessibilitytoinstances/3.3.1.png)

- Tại mục Basic information:

  + Function name: `s3PreprocessFunction`

  + Runtime: chọn Python 3.12 (hoặc Node.js 18.x nếu bạn muốn dùng JavaScript)

- Tại mục Execution role chọn: Use an existing role

- Ở dropdown “Existing role” chọn: LambdaEventProcessingRole

- Nhấn nút Create function 

**Bước 2:** Viết mã xử lý

- Sau khi function được tạo, bạn sẽ được đưa đến trang Code của hàm.

- Trong phần Code source, nhập đoạn mã sau:
```
    export const handler = async (event) => {

    console.log("Received event:", event);

    return {

        statusCode: 200,

        body: 'Preprocessing complete'

      };

    };
```

![S3](/images/3-Accessibilitytoinstances/3.3.2.png)

- Nhấn nút Deploy (góc trên bên phải vùng code)

📌 Sau khi Deploy, Lambda đã sẵn sàng xử lý sự kiện từ S3.

**Bước 3:** test Lambda function trên AWS Console

- Đặt tên test event: "TestS3Preprocess"
 
![S3](/images/3-Accessibilitytoinstances/3.3.3Test.png)

- Nhập nội dung sự kiện JSON
  
```json
{
  "Records": [
    {
      "s3": {
        "bucket": {
          "name": "event-driven-demo-bucket"
        },
        "object": {
          "key": "example.csv"
        }
      }
    }
  ]
}
```

-  Nhấn nút Save và sau đó Test

**Bước 4:** Xem kết quả

- Nếu Lambda chạy thành công, bạn sẽ thấy:

![S3](/images/3-Accessibilitytoinstances/3.3.4kqtest.png)


```json
{
  "statusCode": 200,
  "body": "Preprocessing complete"
}
```

- Và log ở bên dưới sẽ in ra sự kiện bạn vừa gửi:


```
START RequestId: ...
Received event: { ... }
END RequestId: ...
```


✅ Kết luận

Bạn đã test xong Lambda function với sự kiện giả lập. Nếu bạn tích hợp trigger từ S3 sau này, sự kiện thật sẽ có cấu trúc giống mẫu JSON mình cung cấp ở trên.