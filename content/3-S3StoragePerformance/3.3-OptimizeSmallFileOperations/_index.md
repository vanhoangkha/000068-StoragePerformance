---
title : "S3 - Optimize Small File Operations"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 3.3 </b> "
---

#### S3 - Optimize Small File Operations

{{% notice note %}}
Optimize small file operations using parallelism.
This Lab will demonstrate how to increase transactions per second (TPS) while moving small **objects**.
{{% /notice %}}


1. Run the following command to create a text file representing the list of id **object**.

```
seq 1 500 > object_ids
cat object_ids
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0001.png?featherlight=false&width=90pc)

2. Run the following command to create a 1KB file.


```
dd if=/dev/urandom of=1KB.file bs=1 count=0 seek=1K
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0002.png?featherlight=false&width=90pc)

3. Run the following command to upload 500 1KB files to S3 using 5 threads. Record the completion time.

```
time parallel --will-cite -a object_ids -j 5 aws s3 cp 1KB.file s3://${bucket}/run1/{}
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0003.png?featherlight=false&width=90pc)

4. Run the following command to upload 500 1KB files to S3 using 15 threads. Record the completion time.

```
time parallel --will-cite -a object_ids -j 15 aws s3 cp 1KB.file s3://${bucket}/run2/{}
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0004.png?featherlight=false&width=90pc)

5. Run the following command to upload 500 1KB files to S3 using 50 threads. Record the completion time.

```
time parallel --will-cite -a object_ids -j 50 aws s3 cp 1KB.file s3://${bucket}/run3/{}
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0005.png?featherlight=false&width=90pc)

6. Run the following command to upload 500 1KB files to S3 using 100 threads.

```
time parallel --will-cite -a object_ids -j 100 aws s3 cp 1KB.file s3://${bucket}/run4/{}
```

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0006.png?featherlight=false&width=90pc)

7. Access S3 to view data details

![CloudFormation Template](/images/5-OptimizeSmallFileOperations/0007.png?featherlight=false&width=90pc)

{{% notice info %}}
Going from 50 to 100 threads may not lead to better performance. For ease of demonstration, we are using multiple AWS CLI instances to demonstrate a concept. In the real world, developers will create thread buckets much more efficiently than our demonstration approach. It would be reasonable to assume that the added threads will continue to add more performance until another bottleneck such as running out of CPU occurs.
{{% /notice %}}