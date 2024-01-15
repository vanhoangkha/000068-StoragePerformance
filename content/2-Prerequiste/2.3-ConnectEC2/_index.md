---
title: "Connecting to EC2"
date: "`r Sys.Date()`"
weight: 3
chapter: false
pre: "<b>2.3</b>"
---

#### Connecting to EC2

1. **Starting the Connection Process**  
   After configuring the Security Group, begin connecting to EC2.
   - Navigate to the **EC2** interface and select **Instances**.
   - Choose the **SID-performance-instance**.
   - Click on **Connect**.

   ![CloudFormation Template](/images/2.3-connectec2/0001.png?featherlight=false&width=90pc)

2. **Using the Connect to Instance Interface**  
   - Choose **EC2 Instance Connection**.
   - Click on **Connect**.

   ![CloudFormation Template](/images/2.3-connectec2/0002.png?featherlight=false&width=90pc)

3. **Successful EC2 Connection**  
   The connection to EC2 is now established.

   ![CloudFormation Template](/images/2.3-connectec2/0003.png?featherlight=false&width=90pc)

4. **Creating an Access Key After EC2 Connection**  
   Post successful EC2 connection, proceed to create an **Access Key** for AWS CLI configuration.
   - Go to **IAM**.

   ![CloudFormation Template](/images/2.3-connectec2/0004.png?featherlight=false&width=90pc)

5. **Navigating the IAM Interface**  
   - Select **Users**.
   - Choose **SID-lab-user1**.

   ![CloudFormation Template](/images/2.3-connectec2/0005.png?featherlight=false&width=90pc)

6. **In the User Interface**  
   - Click on **Security credentials**.
   - Select **Create access key**.

   ![CloudFormation Template](/images/2.3-connectec2/0006.png?featherlight=false&width=90pc)

7. **Upon Successfully Creating an Access Key**  
   - Choose to **Download .csv file**.
   - Click **Close**.

   ![CloudFormation Template](/images/2.3-connectec2/0007.png?featherlight=false&width=90pc)

8. **Entering Commands in the SSH Interface**  
   Enter the following command:

```
aws configure
```


- Continue with the configuration using the information from the downloaded csv file.

![CloudFormation Template](/images/2.3-connectec2/0008.png?featherlight=false&width=90pc)
