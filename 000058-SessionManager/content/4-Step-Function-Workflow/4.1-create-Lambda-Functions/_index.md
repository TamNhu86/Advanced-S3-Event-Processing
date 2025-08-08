---
title : "Create Additional Lambda Functions (Processing and Storing Results)"
date :  "2025-06-27" 
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

#### Create Lambda to Process File Content (`processFileFunction`)

- Go to the AWS Lambda Console

- Click on "Create function"

- Fill in the following information:

    + Function name: `processFileFunction`

    + Runtime: Python 3.12

    + Execution role: Use existing role → select LambdaEventProcessingRole

![S3](/images/4-Step-Function-Workflow/4.1.png)

- Click "Create function"

In the Code section, paste the following code:
```python
def lambda_handler(event, context):
    print("Processing file content...")
    return {
        "status": "processed",
        "filename": event.get("filename", "unknown")
    }
```

![S3](/images/4-Step-Function-Workflow/4.2.png)

- Click "Deploy"

#### Create Lambda to Store Results (`storeResultFunction`)

- Continue creating another function:

  ![S3](/images/4-Step-Function-Workflow/4.3.png)

- Function name: `storeResultFunction`

- Runtime: Python 3.12

- Execution role: LambdaEventProcessingRole

- Sample code:

```python
def lambda_handler(event, context):
    print("Storing result...")
    print("Input from previous step:", event)
    return {
        "status": "stored",
        "original": event
    }
```

  ![S3](/images/4-Step-Function-Workflow/4.4.png)

- Click "Deploy"
