---
title : "Multi-threading"
date : "`r Sys.Date()`"
weight : 3
chapter : false
pre : " <b> 4.3 </b> "
---

#### Optimize EFS performance using multiple threads

{{% notice info %}}
This Lab will demonstrate how multithreaded access improves throughput and IOPS.
{{% /notice %}}

1. In CLI, run the following command to write 2GB of data to EFS using 1MB block size and 4 threads. Record the time to complete.

```
time seq 0 3 | parallel --will-cite -j 4 dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N)- {} bs=1M count=512 oflag=sync
```

![CloudFormation Template](/images/9-Multithreaded/0001.png?featherlight=false&width=90pc)

2. Run the following command to write 2GB of data to EFS using 1MB block size and 16 threads. Record the time to complete.

```
time seq 0 15 | parallel --will-cite -j 16 dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N)- {} bs=1M count=128 oflag=sync
```


![CloudFormation Template](/images/9-Multithreaded/0002.png?featherlight=false&width=90pc)

3. EFS's distributed data storage design means that multithreaded applications can leverage significant aggregate throughput and IOPS levels. By parallelizing your writes to EFS by increasing the number of threads, you can increase your overall throughput and IOPS for EFS.


![CloudFormation Template](/images/9-Multithreaded/0003.png?featherlight=false&width=90pc)