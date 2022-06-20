---
title : "Khởi tạo CloudFormation Template"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 2.1 </b> "
---

#### Khởi tạo CloudFormation Template

1.  Truy cập vào **[AWS Management Console](https://aws.amazon.com/vi/console/)**

    - Tìm **CloudFormation**
    - Chọn **CloudFormation**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **CloudFormation**

   - Chọn **Create stack**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0002.png?featherlight=false&width=90pc)

3. Trong giao diện **Create stack**

   - Chọn **Template is ready**
   - Chọn ****Amazon S3** URL**
   - Nhập URL: **[**Amazon S3** URL](https://aws-storage-immersion-day.s3.us-west-2.amazonaws.com/sid-base-template.yaml)**
   - Chọn  **Next**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0003.png?featherlight=false&width=90pc)

4. Trong giao diện **Stack name**

   - Nhập **FCJ-S3-LAB** đối với **Stack name**
   - **Lab Modules**, chọn **Deploy S3 Security Lab** và **Deploy Storage Performance Lab** là **true**
   - Chọn **Next**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0004.png?featherlight=false&width=90pc)

5. Chọn **Next**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0005.png?featherlight=false&width=90pc)

6. Xác nhận chọn **Capabilities**

   - Chọn **Create stack**

![CloudFormation Template](/images/2.1-LaunchCloudformation/0006.png?featherlight=false&width=90pc)

7. Đợi khoảng 10 phút, Stack tạo thành công.

![CloudFormation Template](/images/2.1-LaunchCloudformation/0007.png?featherlight=false&width=90pc)

8. Xem **Outputs** sẽ có **PerformanceLabInstance** để sử dụng cho bài lab này. 

![CloudFormation Template](/images/2.1-LaunchCloudformation/0008.png?featherlight=false&width=90pc)



