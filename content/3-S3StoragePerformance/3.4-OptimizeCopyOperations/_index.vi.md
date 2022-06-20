---
title : "Tối ưu hóa hoạt động sao chép"
date :  "`r Sys.Date()`" 
weight : 4
chapter : false
pre : " <b> 3.4  </b> "
---

#### Tối ưu hóa việc sao chép các **object** sang các vị trí khác nhau

1. Chạy lệnh sau để tải xuống tệp 5GB từ **S3 bucket** và tải tệp lên cùng bucket nhưng có tiền tố khác. Ghi lại thời gian để hoàn thành.

```
time (aws s3 cp s3://$bucket/upload1.test 5GB.file; aws s3 cp 5GB.file s3://$bucket/copy/5GB.file)  
```

![CloudFormation Template](/images/6-OptimizeCopyOperations/0001.png?featherlight=false&width=90pc)

2. Chạy lệnh sau để sử dụng PUT Copy (copy-object) để di chuyển tệp. Ghi lại thời gian để hoàn thành. Đừng lo lắng nếu có vẻ như lệnh bị treo. Nó sẽ mất một vài phút.

```
time aws s3api copy-object --copy-source $bucket/upload1.test --bucket $bucket --key copy/5GB-2.file
```


![CloudFormation Template](/images/6-OptimizeCopyOperations/0002.png?featherlight=false&width=90pc)

3. Chạy lệnh sau để sao chép tệp giữa S3 bằng một lệnh duy nhất giữa các vị trí. Ghi lại thời gian để hoàn thành. Đừng lo lắng nếu có vẻ như lệnh bị treo. Nó sẽ mất một vài phút.

```
time aws s3 cp s3://$bucket/upload1.test s3://$bucket/copy/5GB-3.file  
```

![CloudFormation Template](/images/6-OptimizeCopyOperations/0003.png?featherlight=false&width=90pc)


4. Truy cập **S3**


    - Chọn **Buckets**
    - Chọn **sid-security-xxx** bucket
    - Chọn folder **copy/**


![CloudFormation Template](/images/6-OptimizeCopyOperations/0004.png?featherlight=false&width=90pc)

5. Quan sát dữ liệu 

![CloudFormation Template](/images/6-OptimizeCopyOperations/0005.png?featherlight=false&width=90pc)

{{% notice info %}}
Lệnh đầu tiên cần thiết để NHẬN dữ liệu từ S3 trở lại phiên bản EC2 và sau đó PUT dữ liệu trở lại S3 từ phiên bản EC2. Lệnh thứ hai sử dụng PUT COPY nhưng chỉ là luồng đơn. Lệnh thứ ba cũng sử dụng PUT COPY, nhưng cũng sử dụng Trình quản lý chuyển, đa luồng tùy thuộc vào cấu hình AWS CLI. Cả lệnh thứ hai và thứ ba đều thực hiện sao chép giữa các vị trí S3 bên trong S3. Điều này dẫn đến chỉ các lệnh gọi API được thực hiện từ máy chủ EC2 và băng thông truyền dữ liệu chỉ được thực hiện bên trong S3.
{{% /notice %}}





