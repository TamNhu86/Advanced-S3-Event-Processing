---
title: "Create IAM Role for Lambda"
date: "2025-06-27"
weight: 2
chapter: false
pre: " <b> 3.2 </b> "
---

**Step 1:** Open the IAM Role creation page  

Go to **IAM > Roles**.

Click the **"Create role"** button (top right corner).

**Step 2:** Choose Trusted Entity (Lambda service)  

In the **Trusted entity type**, select **"AWS service"**

![S3](/images/3-Accessibilitytoinstances/3.2.1.png)

In the **Use case** section, select **"Lambda"**

Click **Next**

**Step 3:** Attach permission policies  

Search for and select the following 3 policies:

![S3](/images/3-Accessibilitytoinstances/3.2.2.png)

Policy name | Purpose:

- **AmazonS3ReadOnlyAccess**: Allows Lambda to read objects from S3
  
- **CloudWatchLogsFullAccess**: Allows Lambda to write logs to CloudWatch
  
- **AWSStepFunctionsFullAccess**: Allows Lambda to call Step Functions, and vice versa

Click **Next**

**Step 4:** Set name and description  

- **Role name**: `LambdaEventProcessingRole`
  
- **Description** (optional): Role for Lambda functions to access S3, Step Functions and CloudWatch

Click **Create role**

**Step 5:** Verify created Role  

In the list of IAM Roles, find `LambdaEventProcessingRole`

Click the role name to open details

Confirm the following:

![S3](/images/3-Accessibilitytoinstances/3.2.4.png)

- **Trusted entity**: `lambda.amazonaws.com`
- 
- **Policies attached**: Should include all 3 selected above

✅ **Result**  

You have successfully created the IAM Role named `LambdaEventProcessingRole` for the Lambda functions used in the event processing workflow. This role will be assigned to functions such as:

- `s3PreprocessFunction`
  
- `processFileFunction`
  
- `storeResultFunction`
