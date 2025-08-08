---
title : "Clean Up Resources"
date :  "2025-06-27"
weight : 6
chapter : false
pre : " <b> 6. </b> "
---

1. Delete the Step Function State Machine

![S3](/images/6.clean/delete1.png)

  - Go to the Step Functions Console

  - Select `FileProcessingWorkflow`

  - Click **Actions → Delete state machine**

  - Confirm deletion

2. Delete Lambda Functions

![S3](/images/6.clean/delete2.png)

  - Open the Lambda Console

  - Delete the following functions one by one:

    + `s3PreprocessFunction`

    + `processFileFunction`

    + `storeResultFunction`

3. Delete the S3 bucket

![S3](/images/6.clean/emty.png)

  - Select the bucket `event-driven-demo-bucket`
  
  - Empty the bucket
  
  - Delete the S3 bucket

4. Delete the IAM Role (if no longer needed)

![S3](/images/6.clean/deleterole.png)
