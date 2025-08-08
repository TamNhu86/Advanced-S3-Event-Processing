---
title: "Architecture Overview"
date: 2025-06-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

{{% notice info %}}
An AWS account with permissions for S3, Lambda, Step Functions, and IAM is required.
Basic understanding of AWS Lambda and Amazon S3 is expected.
You should know how to create IAM roles, policies, and use the AWS Console or AWS CLI.
{{% /notice %}}

The advanced event processing system is designed based on an event-driven architecture, using serverless components for high scalability and cost optimization.

![S3](/images/2.prerequisite/2.Tongquankientruc.png)

### Step-by-step Event Flow:

1. **Upload file to S3**:  
- A user or external system uploads a file (e.g., image, CSV, JSON, log, etc.) to an S3 bucket.

2. **S3 triggers an event**:  
- Amazon S3 emits an `s3:ObjectCreated:*` event and sends file metadata to either an SNS topic or directly to a Lambda function.

3. **Initial Lambda (preprocessing)**:  
 oThis Lambda function processes metadata, validates format, filters out invalid files, and extracts basic information.

   - If valid → proceed with processing.  
   - If invalid → log the error and terminate.

4. **Step Function orchestration**:  
   
   AWS Step Functions coordinate the entire workflow

5. **Monitoring with CloudWatch**:  
   Each Lambda function logs to CloudWatch Logs.  
   Step Functions can be monitored through execution status and state transitions.

6. **Result Notification**:  
   Final results, whether successful or failed, are sent to users via SNS, email, or logged for review.
