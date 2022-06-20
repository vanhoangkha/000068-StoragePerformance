---
title : "Kích thước I/O và Tần số đồng bộ hóa"
date :  "`r Sys.Date()`" 
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

#### Tối ưu hóa hiệu suất EFS dựa trên Kích thước I / O và Tần suất đồng bộ hóa


{{% notice info %}}
Trong Lab này sẽ chứng minh các kích thước I / O và tần số đồng bộ hóa khác nhau ảnh hưởng như thế nào đến thông lượng tới EFS.
{{% /notice %}}

1. Trong CLI, hãy chạy lệnh sau để ghi tệp 2GB vào EFS bằng cách sử dụng kích thước khối 1MB và đồng bộ hóa một lần sau mỗi tệp. Ghi lại thời gian để hoàn thành.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress conv=fsync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0001.png?featherlight=false&width=90pc)

2. Chạy lệnh sau để ghi tệp 2 GB vào EFS sử dụng kích thước khối 16MB và đồng bộ hóa một lần sau mỗi tệp. Ghi lại thời gian để hoàn thành.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=16M count=128 status=progress conv=fsync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0002.png?featherlight=false&width=90pc)

3. Chạy lệnh sau để ghi tệp 2GB vào EFS sử dụng kích thước khối 1MB và đồng bộ hóa sau mỗi khối. Ghi lại thời gian để hoàn thành.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress oflag=sync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0003.png?featherlight=false&width=90pc)

4. Chạy lệnh sau để ghi tệp 2 GB vào EFS sử dụng kích thước khối 16MB và đồng bộ hóa sau mỗi khối. Ghi lại thời gian để hoàn thành.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=16M count=128 status=progress oflag=sync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0004.png?featherlight=false&width=90pc)

{{% notice note %}}
Đồng bộ hóa sau mỗi khối làm giảm đáng kể hiệu suất của hệ thống tệp. Hiệu suất tối ưu đạt được bằng cách đồng bộ hóa sau mỗi tệp.
{{% /notice %}}

