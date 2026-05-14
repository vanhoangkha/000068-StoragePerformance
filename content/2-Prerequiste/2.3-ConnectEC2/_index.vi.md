---
title : "Kết nổi EC2"
date: 2024-01-01
weight : 3 
chapter : false
pre : " <b> 2.3 </b> "
---

#### Kết nối EC2

1. Sau khi tiến hành cấu hình Security Group. Chúng ta sẽ kết nối EC2.

   - Trong giao diện **EC2**, chọn **Instances**
   - Chọn **SID-performance-instance**
   - Chọn **Connect**

![CloudFormation Template](/images/2.3-connectec2/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **Connect to instance**

    - Chọn **EC2 instance Conect**
    - Chọn **Connect**

![CloudFormation Template](/images/2.3-connectec2/0002.png?featherlight=false&width=90pc)

3. Kết nối **EC2** thành công.

![CloudFormation Template](/images/2.3-connectec2/0003.png?featherlight=false&width=90pc)

4. Sau khi kết nối EC2 thành công. Chúng ta sẽ tạo **Access Key** để cấu hình **AWS CLI**

   - Truy cập vào **IAM**

![CloudFormation Template](/images/2.3-connectec2/0004.png?featherlight=false&width=90pc)

5. Trong giao diện **IAM**

   - Chọn **Users**
   - Chọn **SID-lab-user1**

![CloudFormation Template](/images/2.3-connectec2/0005.png?featherlight=false&width=90pc)

6. Trong giao diện user

   - Chọn **Security credentials**
   - Chọn **Create access key**

![CloudFormation Template](/images/2.3-connectec2/0006.png?featherlight=false&width=90pc)

7. Khi tạo **Access key** thành công

   - Chọn **Download.csv file**
   - Chọn **Close**

![CloudFormation Template](/images/2.3-connectec2/0007.png?featherlight=false&width=90pc)

8. Nhập lệnh trên giao diện **SSH**

```
aws configure
```

   - Tiến hành cấu hình từ thông tin của file csv tải về.

![CloudFormation Template](/images/2.3-connectec2/0008.png?featherlight=false&width=90pc)

