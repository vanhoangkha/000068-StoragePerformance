---
title : "Connect EC2 "
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 2.3 </b> "
---

#### Connect EC2

1. After proceeding to configure Security Group. We will connect EC2.

   - In the **EC2** interface, select **Instances**
   - Select **SID-performance-instance**
   - Select **Connect**

![CloudFormation Template](/images/2.3-connectec2/0001.png?featherlight=false&width=90pc)

2. In the **Connect to instance** interface

    - Select **EC2 instance Connection**
    - Select **Connect**

![CloudFormation Template](/images/2.3-connectec2/0002.png?featherlight=false&width=90pc)

3. **EC2** connection successful.

![CloudFormation Template](/images/2.3-connectec2/0003.png?featherlight=false&width=90pc)

4. After a successful EC2 connection. We will create **Access Key** to configure **AWS CLI**

   - Access to **IAM**

![CloudFormation Template](/images/2.3-connectec2/0004.png?featherlight=false&width=90pc)

5. In the **IAM** interface

   - Select **Users**
   - Select **SID-lab-user1**

![CloudFormation Template](/images/2.3-connectec2/0005.png?featherlight=false&width=90pc)

6. In the user interface

   - Select **Security credentials**
   - Select **Create access key**

![CloudFormation Template](/images/2.3-connectec2/0006.png?featherlight=false&width=90pc)

7. When creating **Access key** successfully

   - Select **Download.csv file**
   - Select **Close**

![CloudFormation Template](/images/2.3-connectec2/0007.png?featherlight=false&width=90pc)

8. Enter commands on the **SSH** interface

```
aws configure
```

   - Proceed to configure from the information of the downloaded csv file.

![CloudFormation Template](/images/2.3-connectec2/0008.png?featherlight=false&width=90pc)