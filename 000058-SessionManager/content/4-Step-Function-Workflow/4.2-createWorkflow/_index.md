---
title : "Create Step Functions Workflow"
date :  "2025-06-27" 
weight : 2 
chapter : false
pre : " <b> 4.2 </b> "
---

1. Access Step Functions

- Go to the AWS Step Functions Console

- Click "Create state machine"

- Enter the name `FileProcessingWorkflow`

![S3](/images/4-Step-Function-Workflow/4.5.png)

- Choose "Author with code snippets"

- Paste the following JSON configuration in the Definition tab:
```
{
  "StartAt": "Process File",
  "States": {
    "Process File": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:<account-id>:function:processFileFunction",
      "Next": "Store Result",
      "Retry": [
        {
          "ErrorEquals": ["States.ALL"],
          "IntervalSeconds": 2,
          "MaxAttempts": 2
        }
      ],
      "Catch": [
        {
          "ErrorEquals": ["States.ALL"],
          "Next": "Fail Handler"
        }
      ]
    },
    "Store Result": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:ap-southeast-1:<account-id>:function:storeResultFunction",
      "End": true
    },
    "Fail Handler": {
      "Type": "Fail",
      "Error": "WorkflowFailed",
      "Cause": "Lambda function failed"
    }
  }
}
```

![S3](/images/4-Step-Function-Workflow/4.6.png)

📌 Explanation:

- Retry: automatically retries the Lambda function if it fails

- Catch: if all retries fail, the execution is redirected to the Fail Handler

2. Create the Workflow

- Click "Next"

- Review the name, role, and permissions

- Click "Create state machine"

![S3](/images/4-Step-Function-Workflow/4.7.png)

![S3](/images/4-Step-Function-Workflow/4.8.png)
