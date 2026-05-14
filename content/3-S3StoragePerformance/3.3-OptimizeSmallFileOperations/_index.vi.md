---
title : "Tối ưu hóa hoạt động tệp nhỏ"
date: 2024-01-01
weight : 3
chapter : false
pre : " <b> 3.3  </b> "
---

#### Tối ưu hóa hoạt động tệp nhỏ

{{% notice note %}}
Tối ưu hóa hoạt động tệp nhỏ bằng cách sử dụng song song.
Trong Lab này sẽ trình bày cách tăng giao dịch mỗi giây (TPS) trong khi di chuyển các **object** nhỏ.
{{% /notice %}}


1. Chạy lệnh sau để tạo tệp văn bản đại diện cho danh sách id **object**.

```
seq 1 500 > object_ids  
cat object_ids 
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0001.png?featherlight=false&width=90pc)

2. Chạy lệnh sau để tạo tệp 1KB.


```
dd if=/dev/urandom of=1KB.file bs=1 count=0 seek=1K  
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0002.png?featherlight=false&width=90pc)

3. Chạy lệnh sau để tải 500 tệp 1KB lên S3 bằng 5 luồng. Ghi lại thời gian hoàn thành.

```
time parallel --will-cite -a object_ids -j 5 aws s3 cp 1KB.file s3://${bucket}/run1/{}
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0003.png?featherlight=false&width=90pc)

4. Chạy lệnh sau để tải lên 500 tệp 1KB lên S3 bằng cách sử dụng 15 luồng. Ghi lại thời gian hoàn thành.

```
time parallel --will-cite -a object_ids -j 15 aws s3 cp 1KB.file s3://${bucket}/run2/{}   
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0004.png?featherlight=false&width=90pc)

5. Chạy lệnh sau để tải lên 500 tệp 1KB lên S3 bằng cách sử dụng 50 luồng. Ghi lại thời gian hoàn thành.

```
time parallel --will-cite -a object_ids -j 50 aws s3 cp 1KB.file s3://${bucket}/run3/{}  
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0005.png?featherlight=false&width=90pc)

6. Chạy lệnh sau để tải lên 500 tệp 1KB lên S3 bằng cách sử dụng 100 luồng.

```
time parallel --will-cite -a object_ids -j 100 aws s3 cp 1KB.file s3://${bucket}/run4/{}  
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0006.png?featherlight=false&width=90pc)

7. Truy cập S3 để xem chi tiết dữ liệu 

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0007.png?featherlight=false&width=90pc)

{{% notice info %}}
Tăng từ 50 đến 100 chủ đề có thể không dẫn đến hiệu suất cao hơn. Để dễ chứng minh, chúng tôi đang sử dụng nhiều phiên bản AWS CLI để thể hiện một khái niệm. Trong thế giới thực, các nhà phát triển sẽ tạo các bucket luồng hiệu quả hơn nhiều so với phương pháp trình diễn của chúng tôi. Sẽ là hợp lý khi giả định rằng các luồng được thêm vào sẽ tiếp tục tăng thêm hiệu suất cho đến khi xảy ra một nút cổ chai khác như hết CPU.
{{% /notice %}}


