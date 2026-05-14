---
title : "Lệnh đồng bộ hóa"
date: 2024-01-01
weight : 2 
chapter : false
pre : " <b> 3.2  </b> "
---

#### Lệnh đồng bộ hóa

{{% notice info %}}
Lệnh đồng bộ s3 đồng bộ hóa nội dung của một bucket và một thư mục hoặc nội dung của hai bucket. Thông thường, đồng bộ hóa s3 sao chép các tệp hoặc **object** bị thiếu hoặc lỗi thời giữa nguồn và đích. Tuy nhiên, bạn cũng có thể cung cấp tùy chọn --delete để xóa các tệp hoặc **object** khỏi đích không có trong nguồn.
{{% /notice %}}

Trong Lab này sẽ sử dụng lệnh đồng bộ aws s3 để di chuyển 2.000 tệp với tổng số xấp xỉ 2 GB dữ liệu.

1. Chạy lệnh sau để thực hiện đồng bộ hóa bằng 1 luồng. Ghi lại thời gian hoàn thành.

```
aws configure set default.s3.max_concurrent_requests 1  
time aws s3 sync /ebs/tutorial/data-1m/ s3://${bucket}/sync1/  
```

![CloudFormation Template](/images/4-SyncCommand/0001.png?featherlight=false&width=90pc)

2. Chạy lệnh sau để thực hiện đồng bộ hóa bằng 10 luồng. Ghi lại thời gian hoàn thành.

```
aws configure set default.s3.max_concurrent_requests 10  
time aws s3 sync /ebs/tutorial/data-1m/ s3://${bucket}/sync2/ 
```

![CloudFormation Template](/images/4-SyncCommand/0002.png?featherlight=false&width=90pc)

{{% notice note %}}
Lưu ý sự giảm thời gian để hoàn tất quá trình đồng bộ hóa s3 bằng 10 luồng. Như bạn có thể thấy, nhiều luồng làm giảm thời gian cần thiết để di chuyển tệp.
{{% /notice %}}

3. Truy cập vào **sid-security-xxx** bucket và chọn **sync1** và **sync2**

![CloudFormation Template](/images/4-SyncCommand/0003.png?featherlight=false&width=90pc)

4. Xem dữ liệu được đồng bộ.

![CloudFormation Template](/images/4-SyncCommand/0004.png?featherlight=false&width=90pc)