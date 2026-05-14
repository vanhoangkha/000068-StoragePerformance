---
title : "Configuring security groups"
date: 2024-01-01
weight : 2
chapter : false
pre : " <b> 2.2 </b> "
---

#### Configure security group

We configure the security group to prepare for the next step of connecting to EC2

1. Access **AWS Management Console**

    - Find **EC2**
    - Select **EC2**

![CloudFormation Template](/images/2.2-securitygroup/0001.png?featherlight=false&width=90pc)

2. In the **EC2** interface

   - Select **Security Group**
   - Select **SID-ssh-sg**
   - Select **Inbound rules**
   - Select **Edit indound rules**

![CloudFormation Template](/images/2.2-securitygroup/0002.png?featherlight=false&width=90pc)

3. Configure **Inbound rules**

   - Select **Add rule**
   - Select **SSH**, Source **Anywhere-IPv4**
   - Select **HTTP**, Source **Anywhere-IPv4**
   - Select **Save rules***

![CloudFormation Template](/images/2.2-securitygroup/0003.png?featherlight=false&width=90pc)

4. Configure **Inbound rules** successfully.

![CloudFormation Template](/images/2.2-securitygroup/0004.png?featherlight=false&width=90pc)