---
title : "Dọn dẹp tài nguyên"
date :  "`r Sys.Date()`" 
weight : 5 
chapter : false
pre : " <b> 5. </b> "
---

#### Dọn dẹp tài nguyên

#### Xóa bucket S3

1. Truy cập vào giao diện [S3]( https://console.aws.amazon.com/s3/)
2. Chọn **Bucket** cần xóa.
3. Chọn **Delete** (phải **Empty** bucket trước khi xóa)
4. Trong trang **Delete bucket**, xác nhận xóa bucket
5. Chọn **Delete bucket**.

#### Xóa CloudFormation Stack

1. Truy cập vào giao diện [CloudFormation](https://console.aws.amazon.com/cloudformation)
2. Chọn **Stack** liên quan bài lab.
3. Chọn **Delete**
4. Xác nhận xóa stack bằng **Delete stack**

#### Terminate EC2

1. Truy cập vào giao diện [EC2](https://console.aws.amazon.com/ec2/)
2. Chọn **Instances**
3. Chọn **Instance state**,  sau đó chọn **Terminate instance**
4. Xác thực **Terminate**

Kiểm tra các tài nguyên khác liên quan bài lab.