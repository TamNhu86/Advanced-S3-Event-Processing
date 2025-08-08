---
title : "Tạo S3 Bucket"
date :  "2025-06-27" 
weight : 1
chapter : false
pre : " <b> 3.1 </b> "
--- 

**Bước 1: Truy cập giao diện tạo bucket** 

- Đảm bảo bạn đang đăng nhập bằng tài khoản AWS và ở vùng Asia Pacific (Singapore) - ap-southeast-1

**Bước 2: Nhập thông tin Bucket** 
 
- Bucket name (tên duy nhất toàn cục):

- Ví dụ: `event-driven-demo-bucket-2025`

Gợi ý: dùng tên ngắn gọn, không chứa khoảng trắng hoặc ký tự đặc biệt

🌍 AWS Region:

Mặc định là Asia Pacific (Singapore) ap-southeast-1 — giữ nguyên nếu bạn dùng cùng vùng cho Lambda, Step Functions

**Bước 3: Thiết lập Public Access**

- Trong mục Block Public Access settings for this bucket:

![S3](/images/3-Accessibilitytoinstances/01.png)



✅ Bỏ tick ở dòng: Block all public access

- AWS sẽ hiện cảnh báo → bạn tick vào ô xác nhận “I acknowledge…”

📌 Lý do: Bạn cần bật quyền truy cập trong một số tình huống như tải tệp hoặc tích hợp Lambda (có thể giới hạn bằng IAM policy sau này)

**Bước 4: Bucket Versioning (tuỳ chọn)**

- Nếu không cần theo dõi lịch sử phiên bản file, chọn Disable

- Nếu bạn muốn bật tính năng khôi phục file cũ, chọn Enable

**Bước 5: Tags (tuỳ chọn)**

- Có thể thêm tags như:

- Project: S3EventWorkshop

- Owner: your-name

- Không bắt buộc, nhưng giúp quản lý chi phí & lọc báo cáo tốt hơn.

**Bước 6: Encryption**

- Bạn có thể chọn:

- Disable (nếu chỉ test)

- Hoặc S3-managed keys (SSE-S3) nếu muốn mã hóa mặc định cho mọi tệp

**Bước 7: Advanced Settings**

- Không cần thay đổi nếu bạn chỉ sử dụng cho mục đích xử lý sự kiện. Để mặc định.

**Bước 8: Nhấn “Create bucket”**

- Xem lại toàn bộ thiết lập

- Cuối trang → nhấn Create bucket