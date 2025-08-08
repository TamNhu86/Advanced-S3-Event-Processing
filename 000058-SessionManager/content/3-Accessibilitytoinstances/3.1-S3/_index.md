---
title: "Create S3 Bucket"
date: "2025-06-27"
weight: 1
chapter: false
pre: " <b> 3.1 </b> "
---

**Step 1: Access the bucket creation interface**  

Make sure you're logged in to your AWS account and selected the **Asia Pacific (Singapore)** region — `ap-southeast-1`.

**Step 2: Enter Bucket Information** 

**Bucket name** (must be globally unique): 

Example: `event-driven-demo-bucket-2025`  

Tip: Use a short name, avoid spaces or special characters.

🌍 **AWS Region**:  

Default is **Asia Pacific (Singapore) – ap-southeast-1** — keep this if you're using the same region for Lambda and Step Functions.

**Step 3: Configure Public Access Settings**  

In the **Block Public Access settings for this bucket**:

![S3](/images/3-Accessibilitytoinstances/01.png)

✅ Uncheck: **Block all public access**

AWS will show a warning → check the box to acknowledge:

**“I acknowledge that the current settings might result in this bucket and the objects within becoming public.”**

📌 Reason: You may need public access in some scenarios such as downloading files or Lambda integrations (you can later restrict access using IAM policies).

**Step 4: Bucket Versioning (optional)**  

- Select **Disable** if you don’t need file version tracking.  
  
- Select **Enable** if you want to be able to restore previous versions of files.

**Step 5: Tags (optional)**  

You may add tags such as:  

- `Project`: `S3EventWorkshop`  
  
- `Owner`: `your-name`  

Not required, but helpful for cost tracking and report filtering.

**Step 6: Encryption**  

Choose one of the following:

- **Disable** (if you're only testing), or 
-  
- **S3-managed keys (SSE-S3)** for automatic encryption of all uploaded files.

**Step 7: Advanced Settings**  

No changes needed if this bucket is only for event processing purposes. Keep default settings.

**Step 8: Click “Create bucket”**  

Review all settings.  

Scroll to the bottom → click **Create bucket**.
