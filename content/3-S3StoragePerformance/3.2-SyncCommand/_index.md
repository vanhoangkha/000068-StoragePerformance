---
title : "Sync command"
date: 2024-01-01
weight : 2
chapter : false
pre : " <b> 3.2 </b> "
---

#### Synchronization command

{{% notice info %}}
The s3 sync command synchronizes the contents of a bucket and a directory or the contents of two buckets. Usually, s3 sync copies missing or outdated files or **objects between source and destination. However, you can also provide the --delete option to remove files or **object** from the destination that is not present in the source.
{{% /notice %}}

This Lab will use the aws s3 sync command to move 2,000 files for a total of approximately 2 GB of data.

1. Run the following command to do 1-thread synchronization. Record the completion time.

```
aws configure set default.s3.max_concurrent_requests 1
time aws s3 sync /ebs/tutorial/data-1m/ s3://${bucket}/sync1/
```

![CloudFormation Template](/images/4-SyncCommand/0001.png?featherlight=false&width=90pc)

2. Run the following command to perform synchronization using 10 threads. Record the completion time.

```
aws configure set default.s3.max_concurrent_requests 10
time aws s3 sync /ebs/tutorial/data-1m/ s3://${bucket}/sync2/
```

![CloudFormation Template](/images/4-SyncCommand/0002.png?featherlight=false&width=90pc)

{{% notice note %}}
Notice the reduction in the time it takes to complete the s3 sync by 10 threads. As you can see, multiple threads reduce the time it takes to move files.
{{% /notice %}}

3. Go to **sid-security-xxx** bucket and select **sync1** and **sync2**

![CloudFormation Template](/images/4-SyncCommand/0003.png?featherlight=false&width=90pc)

4. View synchronized data.

![CloudFormation Template](/images/4-SyncCommand/0004.png?featherlight=false&width=90pc)