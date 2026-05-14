---
title : "Mô-đun Giao thức tệp"
date: 2024-01-01
weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

#### So sánh các giao thức truyền tệp phổ biến

{{% notice info %}}
Trong Lab này sẽ so sánh hiệu suất của các tiện ích truyền tệp khác nhau và EFS.
{{% /notice %}}

1. Trong CLI, hãy chạy các lệnh sau để xác minh phiên bản EC2 có khối lượng xấp xỉ 2GB EBS.

```
du -csh /ebs/tutorial/data-1m/  
```


![CloudFormation Template](/images/10-Underconstruction/0001.png?featherlight=false&width=90pc)

2. Chạy các lệnh sau để xác minh phiên bản EC2 có 2000 tệp trong ổ đĩa EBS.

```
find /ebs/tutorial/data-1m/. -type f | wc -l
```


![CloudFormation Template](/images/10-Underconstruction/0002.png?featherlight=false&width=90pc)

3. Chạy các lệnh sau để chuyển tệp từ EBS sang EFS bằng rsync. Ghi lại thời gian hoàn thành. Lệnh sẽ mất một vài phút để hoàn thành, đừng lo lắng nếu lệnh này bị treo.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time rsync -r /ebs/tutorial/data-1m/ /efs/tutorial/rsync/
```


![CloudFormation Template](/images/10-Underconstruction/0003.png?featherlight=false&width=90pc)

4. Chạy các lệnh sau để chuyển tệp từ EBS sang EFS bằng lệnh sao chép. Ghi lại thời gian hoàn thành. Lệnh sẽ mất một vài phút để hoàn thành, đừng lo lắng nếu lệnh này bị treo.


```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time cp -r /ebs/tutorial/data-1m/* /efs/tutorial/cp/
```


![CloudFormation Template](/images/10-Underconstruction/0004.png?featherlight=false&width=90pc)

5. Chạy các lệnh sau để đặt biến $ thread thành 4 luồng cho mỗi CPU.

```
threads=$(($(nproc --all) * 4))
echo $threads
```


![CloudFormation Template](/images/10-Underconstruction/0005.png?featherlight=false&width=90pc)

6. Chạy các lệnh sau để chuyển tệp từ EBS sang EFS bằng fpsync. Ghi lại thời gian hoàn thành. Lệnh sẽ mất một vài phút để hoàn thành.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time fpsync -n ${threads} -v /ebs/tutorial/data-1m/ /efs/tutorial/fpsync/
```


![CloudFormation Template](/images/10-Underconstruction/0006.png?featherlight=false&width=90pc)

7. Chạy các lệnh sau để chuyển tệp từ EBS sang EFS bằng cp + GNU Parallel. Ghi lại thời gian hoàn thành. Lệnh sẽ mất một vài phút để hoàn thành.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time find /ebs/tutorial/data-1m/. -type f | parallel --will-cite -j ${threads} cp {} /efs/tutorial/parallelcp
```

![CloudFormation Template](/images/10-Underconstruction/0007.png?featherlight=false&width=90pc)


{{% notice note %}}
Không phải tất cả các tiện ích chuyển tệp đều hoạt động tương tự. Hệ thống tệp được phân phối trên một số lượng máy chủ lưu trữ không bị giới hạn và thiết kế lưu trữ dữ liệu phân tán này có nghĩa là các ứng dụng đa luồng như fpsync, mcp và GNU song song có thể thúc đẩy mức thông lượng và IOPS đáng kể đến EFS khi so sánh với các ứng dụng đơn luồng.
{{% /notice %}}

