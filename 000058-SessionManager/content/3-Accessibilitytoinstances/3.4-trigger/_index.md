---
title : "Set Up Trigger from S3 to Lambda"
date :  "2025-06-27" 
weight : 5
chapter : false
pre : " <b> 3.4 </b> "
--- 
**Step 1:**

- Locate and click the name of the bucket you created (e.g., event-driven-demo-bucket)
  
    + Create a folder named `uploads` and upload a `.jpg` file
  
    ![S3](/images/3-Accessibilitytoinstances/3.3.5folderupload.png)

    ![S3](/images/3-Accessibilitytoinstances/3.3.6upload.png)
  
- Open the event configuration section
  
    + In the bucket interface → go to the **Properties** tab

    + Scroll down to the **Event notifications** section

    + Click “Create event notification”

- Configure the event trigger
  
    + Enter a name, e.g., `TriggerLambdaOnUpload`
  
     ![S3](/images/3-Accessibilitytoinstances/3.3.7createeventnotification.png)

    + Check: ✅ All object create events (or just PUT if you only want to trigger on upload)

    ![S3](/images/3-Accessibilitytoinstances/3.3.8event.png)

- Prefix and suffix (optional):

    + **Prefix** (optional): e.g., `uploads/` to monitor a specific folder

    + **Suffix** (optional): `.csv` to process only CSV files

    (In this example we use a suffix filter)

- Destination:
  
    ![S3](/images/3-Accessibilitytoinstances/3.3.9.png)

    + Select: Lambda function

    + Function name: `s3PreprocessFunction` (you can select it from the dropdown)

- Save configuration: Click **Save changes**


✅ **Result**

- Every time you upload a file to the bucket, the `s3PreprocessFunction` Lambda will automatically be triggered.

- You can view logs in **CloudWatch Logs** after each upload.

🎯 **Verification**

- Try uploading a `.txt` or `.csv` file to the bucket via the AWS Console

- Open **AWS CloudWatch Logs** → find log group `/aws/lambda/s3PreprocessFunction`

- Look for the latest log entry → you should see output similar to this:
  
  ![S3](/images/3-Accessibilitytoinstances/3.3.10output.png)
