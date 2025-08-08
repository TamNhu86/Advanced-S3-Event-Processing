---
title : "Creating Alerts with CloudWatch Alarm"
date :  "2025-06-27" 
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Alert when Lambda fails multiple times

- Go to the CloudWatch Console

- In the left menu, select **Alarms** → **All alarms** → **Create alarm**

- Click **Select metric**

![S3](/images/5.fwd/createalarms.png)

- Navigate:

  - Browse → choose **Lambda**
  - → **By Function Name**
  - → select function `processFileFunction`

![S3](/images/5.fwd/unctionname.png)

- Select the **Errors** metric → **Select metric**

![S3](/images/5.fwd/erro.png)

- Set conditions:

  + **Statistic**: Sum

  + **Period**: 5 minutes

  + **Threshold type**: Static

  + **Define threshold**: Greater than 1

![S3](/images/5.fwd/5.02.01.png)

- Click **Next**

- Set notification actions:

  - **Notification**:

    - Choose or create SNS Topic (if none, select “Create new topic”)

![S3](/images/5.fwd/5.02.02.png)

    - Enter the email address to receive alerts

    - After creation, **confirm the subscription email** sent by AWS

![S3](/images/5.fwd/5.02.03.png)

- Name the alarm: `LambdaErrorAlarm`

![S3](/images/5.fwd/5.02.04.png)

- Click **Create alarm**

---

#### Alert when Step Function fails

**Step 1: Access Step Functions Metrics**

- In AWS Console: open CloudWatch

  + Go to **Metrics** → select **Browse**

![S3](/images/5.fwd/5.03.01.png)

  + Choose service group **States** → then **Execution Metrics**

![S3](/images/5.fwd/5.03.02.png)

  + Locate metric: **ExecutionsFailed** for the state machine `FileProcessingWorkflow`

**Step 2: Create Alarm**

![S3](/images/5.fwd/5.03.03.png)

  + Tick the row **ExecutionsFailed**

  + Click **Create alarm** (top-right)

**Step 3: Set condition**

![S3](/images/5.fwd/5.03.04.png)

  + **Metric**: ExecutionsFailed

  + **Statistic**: Sum

  + **Period**: 5 minutes

  + **Condition**: Greater than 0

  + **Threshold type**: Static

**Step 4: Assign Notification Action**

![S3](/images/5.fwd/5.03.05.png)

  + Choose **In alarm**

  + Select previously created SNS Topic to receive email

  + If none exists, click **Create new topic**, enter email, and confirm AWS subscription email

**Step 5: Name and create alarm**

![S3](/images/5.fwd/5.03.06.png)

  + **Alarm name**: `StepFunctionFailureAlarm`

  + Click **Next**, then **Create alarm**

![S3](/images/5.fwd/5.03.07.png)

✅ **Result**: After setup, the system will monitor and alert if the Step Function fails within a 5-minute interval.

✅ **Post-configuration result**:

- CloudWatch logs all Lambda functions and Step Functions

- Alarms send emails if the system encounters errors

- Enables easier monitoring and quick response if the workflow breaks
