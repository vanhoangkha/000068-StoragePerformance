---
title: "Launch CloudFormation Template"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b> 2.1 </b>"
---

#### Launch CloudFormation Template

1. Go to the **[AWS Management Console](https://aws.amazon.com/en/console/)**

    - Find **CloudFormation**
    - Select **CloudFormation**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0001.png?featherlight=false&width=90pc)

2. In the **CloudFormation** interface:

   - Select **Create stack**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0002.png?featherlight=false&width=90pc)

3. In the **Create stack** interface:

   - Select **Template is ready**
   - Select **Amazon S3 URL**
   - Enter URL: **[Amazon S3 URL](https://aws-storage-immersion-day.s3.us-west-2.amazonaws.com/sid-base-template.yaml)**
   - Select **Next**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0003.png?featherlight=false&width=90pc)

4. In the **Stack name** interface:

   - Enter **FCJ-S3-LAB** for **Stack name**
   - Under **Lab Modules**, select **Deploy S3 Security Lab** and **Deploy Storage Performance Lab** as **true**
   - Select **Next**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0004.png?featherlight=false&width=90pc)

5. Select **Next**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0005.png?featherlight=false&width=90pc)

6. Confirm **Capabilities**:

   - Select **Create stack**

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0006.png?featherlight=false&width=90pc)

7. Wait about 10 minutes for the Stack to be created successfully.

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0007.png?featherlight=false&width=90pc)

8. View the **Outputs** which will include **PerformanceLabInstance** for use in this lab.

    ![CloudFormation Template](/images/2.1-LaunchCloudformation/0008.png?featherlight=false&width=90pc)
