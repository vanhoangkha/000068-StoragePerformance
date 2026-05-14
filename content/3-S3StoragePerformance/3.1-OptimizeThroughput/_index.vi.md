---
title : "Tối ưu hóa thông lượng"
date: 2024-01-01
weight : 1 
chapter : false
pre : " <b> 3.1  </b> "
---

#### Tối ưu hóa thông lượng

{{% notice note %}}
Trong Lab này chứng minh rằng khối lượng công việc có thể được song song bằng cách chia nhỏ một **object** lớn thành nhiều phần hoặc bằng cách có các tệp nhỏ hơn.
{{% /notice %}}

1. Trong phiên SSH của bạn, hãy chạy lệnh sau để định cấu hình cài đặt AWS CLI S3.

```
aws configure set default.s3.max_concurrent_requests 1  
aws configure set default.s3.multipart_threshold 64MB  
aws configure set default.s3.multipart_chunksize 16MB  
```

![CloudFormation Template](/images/3-OptimizeThroughput/0001.png?featherlight=false&width=90pc)

2. Trình quản lý chuyển giao có thể tối ưu hóa quá trình truyền. aws s3api chỉ đơn giản thực hiện cuộc gọi api cụ thể mà bạn đã chỉ định.


```
cat ~/.aws/config  
```

![CloudFormation Template](/images/3-OptimizeThroughput/0002.png?featherlight=false&width=90pc)

3. Chạy lệnh sau để tạo tệp **5GB**.

```
dd if=/dev/urandom of=5GB.file bs=1 count=0 seek=5G 
```

![CloudFormation Template](/images/3-OptimizeThroughput/0003.png?featherlight=false&width=90pc)

4. Chạy lệnh sau để tải tệp 5 GB lên **S3 bucket** bằng cách sử dụng 1 luồng. Ghi lại thời gian để hoàn thành.

```
time aws s3 cp 5GB.file s3://${bucket}/upload1.test    
```

![CloudFormation Template](/images/3-OptimizeThroughput/0004.png?featherlight=false&width=90pc)

5. Chạy lệnh sau để tải tệp 5 GB lên **S3 bucket** bằng cách sử dụng 2 luồng. Ghi lại thời gian để hoàn thành.

```
aws configure set default.s3.max_concurrent_requests 2  
time aws s3 cp 5GB.file s3://${bucket}/upload2.test  
```

![CloudFormation Template](/images/3-OptimizeThroughput/0005.png?featherlight=false&width=90pc)

6. Chạy lệnh sau để tải tệp 5 GB lên **S3 bucket** bằng cách sử dụng 10 luồng. Ghi lại thời gian để hoàn thành.

```
aws configure set default.s3.max_concurrent_requests 10  
time aws s3 cp 5GB.file s3://${bucket}/upload3.test  
```

![CloudFormation Template](/images/3-OptimizeThroughput/0006.png?featherlight=false&width=90pc)

7. Chạy lệnh sau để tải tệp 5 GB lên **S3 bucket** bằng cách sử dụng 20 luồng. Ghi lại thời gian để hoàn thành.

```
aws configure set default.s3.max_concurrent_requests 20   
time aws s3 cp 5GB.file s3://${bucket}/upload4.test  
```

![CloudFormation Template](/images/3-OptimizeThroughput/0007.png?featherlight=false&width=90pc)

{{% notice note %}}
Tại một số điểm, AWS CLI sẽ giới hạn hiệu suất có thể đạt được. Điều này có thể xảy ra nếu bạn không thấy bất kỳ sự gia tăng hiệu suất nào từ 10 đến 20 luồng. Đây là một hạn chế của CLI, việc tăng số luồng lên 100 bằng cách sử dụng phần mềm khác sẽ tiếp tục tăng hiệu suất.

{{% /notice %}}


8. Truy cập vào S3

- Chọn **sid-security-xxx**
- Quan sát các file đã upload.

![CloudFormation Template](/images/3-OptimizeThroughput/0008.png?featherlight=false&width=90pc)

{{% notice note %}}
Dữ liệu cũng có thể được phân đoạn thành nhiều phần. Bước tiếp theo sẽ chứng minh việc di chuyển 5 GB dữ liệu bằng cách sử dụng nhiều tệp nguồn.
{{% /notice %}}

9. Chạy lệnh sau để tạo tệp 1GB.

```
dd if=/dev/urandom of=1GB.file bs=1 count=0 seek=1G
``` 

![CloudFormation Template](/images/3-OptimizeThroughput/0009.png?featherlight=false&width=90pc)


10. Chạy lệnh sau để tải 5GB dữ liệu lên S3 bằng cách tải lên song song năm tệp 1GB. Ghi lại thời gian hoàn thành.

```
time seq 1 5 | parallel --will-cite -j 5 aws s3 cp 1GB.file s3://${bucket}/parallel/object{}.test 
```

![CloudFormation Template](/images/3-OptimizeThroughput/00010.png?featherlight=false&width=90pc)

{{% notice note %}}
Cờ -j là số lượng công việc đồng thời sẽ chạy. Điều này dẫn đến tổng số 100 luồng (20 từ cấu hình aws nhân với 5 công việc).
{{% /notice %}}


11. Tiếp tục truy cập vào S3

- Chọn **sid-security-xxx**
- Chọn **parallel/**

![CloudFormation Template](/images/3-OptimizeThroughput/00011.png?featherlight=false&width=90pc)

12. Chúng ta sẽ thấy tệp **5G** đã được chia thành 5 tệp **1G**

![CloudFormation Template](/images/3-OptimizeThroughput/00012.png?featherlight=false&width=90pc)

{{% notice note %}}
Trong Lab này cho thấy rằng khối lượng công việc có thể được song song bằng cách chia nhỏ một **object** lớn thành nhiều phần hoặc bằng cách có các tệp nhỏ hơn. Một điểm cân bằng cần lưu ý là mỗi PUT được lập hóa đơn ở mức 0,005 đô la cho mỗi 1.000 yêu cầu. Khi bạn chia nhỏ một tệp 5GB thành các phần 16MB, điều đó dẫn đến 313 PUT thay vì 1 PUT. Về cơ bản, bạn có thể xem nó như trả phí để đi nhanh hơn.
{{% /notice %}}

