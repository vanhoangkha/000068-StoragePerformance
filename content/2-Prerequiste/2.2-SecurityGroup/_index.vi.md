---
title : "Cấu hình security group"
date: 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Cấu hình security group

Chúng ta thực hiện cấu hình security group để chuẩn bị cho bước tiếp theo kết nối EC2

1. Truy cập **AWS Management Console**

    - Tìm **EC2**
    - Chọn **EC2**

![CloudFormation Template](/images/2.2-securitygroup/0001.png?featherlight=false&width=90pc)

2. Trong giao diện **EC2**

   - Chọn **Security Group**
   - Chọn **SID-ssh-sg** 
   - Chọn **Inbound rules**
   - Chọn **Edit indound rules**

![CloudFormation Template](/images/2.2-securitygroup/0002.png?featherlight=false&width=90pc)

3. Thực hiện cấu hình **Inbound rules**

   - Chọn **Add rule**
   - Chọn **SSH**, Source **Anywhere-IPv4**
   - Chọn **HTTP**, Source **Anywhere-IPv4**
   - Chọn **Save rules***

![CloudFormation Template](/images/2.2-securitygroup/0003.png?featherlight=false&width=90pc)

4. Cấu hình **Inbound rules** thành công.

![CloudFormation Template](/images/2.2-securitygroup/0004.png?featherlight=false&width=90pc)