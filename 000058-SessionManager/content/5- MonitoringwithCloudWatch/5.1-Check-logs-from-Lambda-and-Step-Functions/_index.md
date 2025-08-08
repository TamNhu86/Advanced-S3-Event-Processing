---
title : "Check Logs from Lambda and Step Functions"
date :  "2025-06-27" 
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### Logs from Lambda Function

- Open the CloudWatch Console

- Select Logs → Log groups

- Search for function names: /aws/lambda/s3PreprocessFunction, processFileFunction, storeResultFunction

![S3](/images/3-Accessibilitytoinstances/3.3.10output.png)

- Click the log group → then click on a log stream to view the details of each invocation

#### Logs from Step Function

- Go back to the Step Functions Console

- Select the state machine: `FileProcessingWorkflow`

- Click on any execution → the Execution events tab will show details:

- Input/Output of each step

![S3](/images/5.fwd/5.3.png)

![S3](/images/5.fwd/5.4.png)

- Success/failure status:

![S3](/images/5.fwd/5.3.1.png)

- Error message if any

![S3](/images/5.fwd/5.erro.png)
