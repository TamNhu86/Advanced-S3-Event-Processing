---
title : "Test Alarm"
date :  "2025-06-27"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Test 1: Triggering Alarm When Lambda Fails Multiple Times

🎯 Objective:
Trigger the configured CloudWatch Alarm for `processFileFunction` (or the Lambda function you chose), by intentionally causing it to fail multiple times within 5 minutes.
s
- **Step 1: Modify Lambda to Force an Error**

  ![S3](/images/5.fwd/test01.png)

  + Go to AWS Lambda Console

  + Open the Lambda function (`processFileFunction`)

  + Select the **Code** tab

  + Replace code as follows (Node.js or Python) to always throw an error:

For Python:
```python
def lambda_handler(event, context):
    raise Exception("Forced test error")
```

  + Click **Deploy** to apply changes

- **Step 2: Invoke Lambda Repeatedly to Generate Errors**

  ![S3](/images/5.fwd/test02.png)

  + In Lambda Console → go to the **Test** tab

  + Create a test event:
```json
{
  "test": true
}
```

  + Click **Test** 3–5 times within 1–2 minutes

📌 Goal: Multiple failed invocations → total Errors > 1 in 5 minutes

  ![S3](/images/5.fwd/test03.png)

  ![S3](/images/5.fwd/test04.png)

- **Step 3: Monitor the Alarm**

  + Go to **CloudWatch → Alarms**

  ![S3](/images/5.fwd/test05.png)

  + Check if the `LambdaErrorAlarm` transitions from **OK** to **ALARM** (may take a few minutes)

  + Check your email for alert if linked with SNS Topic

  ![S3](/images/5.fwd/thongbaotest01.png)

---

#### Test 2: Triggering Alarm When Step Function Fails

- **Step 1: Access Step Functions Console**

  + Open `FileProcessingWorkflow`

  + Click “**Start execution**”

  ![S3](/images/5.fwd/testreal.png)

  Enter the following input (depending on your code, but use one that causes Lambda to fail):
```json
{
  "simulateError": true
}
```

If your Lambda does not process input, just make the Lambda step throw an exception by default.

Run the workflow → it should fail

  ![S3](/images/5.fwd/fail.png)

  Check the Execution status: it should show **Failed**

- **Step 2: After Execution Fails**

  + Wait about 1–5 minutes

  + CloudWatch will update the `ExecutionsFailed` metric

  ![S3](/images/5.fwd/erroalarm.png)

- **Step 3: Check the Alarm**

  + Go back to **CloudWatch → Alarms**

  + If `StepFunctionFailureAlarm` moves from ❔ Insufficient data to 🔴 In alarm, your test is successful

  ![S3](/images/5.fwd/erroalarm2.png)

  + Check your email (if you attached the SNS topic and confirmed the subscription):

You will receive an alert about the Step Function failure

  ![S3](/images/5.fwd/tbreal.png)