---
title : " Tối ưu hóa IOPS"
date: 2024-01-01
weight : 1 
chapter : false
pre : " <b> 4.1 </b> "
---

#### Tối ưu hóa EFS IOPS bằng nhiều luồng


{{% notice info %}}
Trong Lab này sẽ trình bày các phương pháp tạo 1.024 tệp khác nhau và so sánh hiệu suất của từng phương pháp.
{{% /notice %}}


1. Trong CLI, hãy chạy lệnh sau để tạo 1.024 tệp không byte. Ghi lại thời gian để hoàn thành.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")    
mkdir -p /efs/tutorial/touch/${directory}  
time for i in {1..1024}; do  
touch /efs/tutorial/touch/${directory}/test-1.3-$i;  
done;
```

![CloudFormation Template](/images/7-OptimizeIOPS/0001.png?featherlight=false&width=90pc)

2. Trong CLI, hãy chạy lệnh sau để tạo 1.024 tệp không byte sử dụng nhiều luồng. Ghi lại thời gian để hoàn thành.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")    
mkdir -p /efs/tutorial/touch/${directory}    
time seq 1 1024 | parallel --will-cite -j 128 touch /efs/tutorial/touch/${directory}/test-1.4-{}
```

![CloudFormation Template](/images/7-OptimizeIOPS/0002.png?featherlight=false&width=90pc)

3. Trong CLI, hãy chạy lệnh sau để tạo 1.024 tệp không byte trong nhiều thư mục bằng cách sử dụng nhiều luồng. Ghi lại thời gian để hoàn thành.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")   
mkdir -p /efs/tutorial/touch/${directory}/{1..32}  
time seq 1 32 | parallel --will-cite -j 32 touch /efs/tutorial/touch/${directory}/{}/test1.5{1..32}
```

![CloudFormation Template](/images/7-OptimizeIOPS/0003.png?featherlight=false&width=90pc)

4. Truy cập vào **Elastic File System**

   - Chọn **File systems**
   - Chọn **SID-efs**

![CloudFormation Template](/images/7-OptimizeIOPS/0004.png?featherlight=false&width=90pc)

5. Cách tốt nhất để tận dụng thiết kế lưu trữ dữ liệu phân tán của **Amazon EFS** là sử dụng song song nhiều luồng và inode.

![CloudFormation Template](/images/7-OptimizeIOPS/0005.png?featherlight=false&width=90pc)






