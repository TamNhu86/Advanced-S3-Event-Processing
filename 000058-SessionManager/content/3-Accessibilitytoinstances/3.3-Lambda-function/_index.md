---
title : "Create Lambda Function: Preprocessing"
date :  "2025-06-27" 
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

**Step 1:** Access the Lambda Console

- Click “Create function”

- Configure the Lambda Function

![S3](/images/3-Accessibilitytoinstances/3.3.1.png)

- Under Basic information:

  + Function name: `s3PreprocessFunction`

  + Runtime: choose Python 3.12 (or Node.js 18.x if you prefer JavaScript)

- Under Execution role, select: Use an existing role

- From the “Existing role” dropdown, choose: LambdaEventProcessingRole

- Click the Create function button

**Step 2:** Write handler code  
After the function is created, you'll be redirected to the Code tab.

In the Code source section, enter the following code:

```javascript
export const handler = async (event) => {
    console.log("Received event:", event);
    return {
        statusCode: 200,
        body: 'Preprocessing complete'
    };
};
```

![S3](/images/3-Accessibilitytoinstances/3.3.2.png)

Click the Deploy button (top right of the code editor)

📌 Once deployed, your Lambda is ready to process events from S3.

**Step 3:** Test the Lambda function on AWS Console

- Name the test event: "TestS3Preprocess"

![S3](/images/3-Accessibilitytoinstances/3.3.3Test.png)

- Paste the following sample event JSON:
```json
{
  "Records": [
    {
      "s3": {
        "bucket": {
          "name": "event-driven-demo-bucket"
        },
        "object": {
          "key": "example.csv"
        }
      }
    }
  ]
}
```

- Click Save and then Test

**Step 4:** Review the result

If the Lambda executes successfully, you will see:

![S3](/images/3-Accessibilitytoinstances/3.3.4kqtest.png)

```json
{
  "statusCode": 200,
  "body": "Preprocessing complete"
}
```

And the logs below will print the event:

```
START RequestId: ...
Received event: { ... }
END RequestId: ...
```

✅ Conclusion

You have successfully tested the Lambda function with a simulated event.  
If you later integrate the trigger from S3, the real event will have a structure similar to the JSON sample provided above.
