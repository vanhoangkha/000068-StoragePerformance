---
title : "Đa luồng"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

#### Tối ưu hóa hiệu suất EFS bằng cách sử dụng nhiều luồng

{{% notice info %}}
Trong Lab này sẽ chứng minh cách truy cập đa luồng cải thiện thông lượng và IOPS.
{{% /notice %}}

1. Trong CLI, hãy chạy lệnh sau để ghi 2GB dữ liệu vào EFS bằng cách sử dụng kích thước khối 1MB và 4 luồng. Ghi lại thời gian để hoàn thành.

```
time seq 0 3 | parallel --will-cite -j 4 dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N)-{} bs=1M count=512 oflag=sync
```

![CloudFormation Template](/images/9-Multithreaded/0001.png?featherlight=false&width=90pc)

2. Chạy lệnh sau để ghi 2GB dữ liệu vào EFS bằng cách sử dụng kích thước khối 1MB và 16 luồng. Ghi lại thời gian để hoàn thành.

```
time seq 0 15 | parallel --will-cite -j 16 dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N)-{} bs=1M count=128 oflag=sync  
```


![CloudFormation Template](/images/9-Multithreaded/0002.png?featherlight=false&width=90pc)

3. Thiết kế lưu trữ dữ liệu phân tán của EFS có nghĩa là các ứng dụng đa luồng có thể thúc đẩy các mức thông lượng tổng hợp và IOPS đáng kể. Bằng cách song song ghi của bạn vào EFS bằng cách tăng số lượng luồng, bạn có thể tăng thông lượng tổng thể và IOPS cho EFS.


![CloudFormation Template](/images/9-Multithreaded/0003.png?featherlight=false&width=90pc)

