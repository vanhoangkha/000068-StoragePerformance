---
title : "I/O Size and Sync Frequency"
date : "`r Sys.Date()`"
weight : 2
chapter : false
pre : " <b> 4.2 </b> "
---

#### Optimize EFS performance based on I/O Size and Sync Frequency


{{% notice info %}}
This Lab will demonstrate how different I/O sizes and synchronization frequencies affect throughput to EFS.
{{% /notice %}}

1. In the CLI, run the following command to write a 2GB file to EFS using a 1MB block size and sync once after each file. Record the time to complete.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress conv=fsync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0001.png?featherlight=false&width=90pc)

2. Run the following command to write 2 GB file to EFS using 16MB block size and sync once after each file. Record the time to complete.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=16M count=128 status=progress conv=fsync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0002.png?featherlight=false&width=90pc)

3. Run the following command to write 2GB file to EFS using 1MB block size and sync after each block. Record the time to complete.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=1M count=2048 status=progress oflag=sync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0003.png?featherlight=false&width=90pc)

4. Run the following command to write 2 GB file to EFS using 16MB block size and sync after each block. Record the time to complete.

```
time dd if=/dev/zero of=/efs/tutorial/dd/2G-dd-$(date +%Y%m%d%H%M%S.%3N) bs=16M count=128 status=progress oflag=sync
```

![CloudFormation Template](/images/8-IOSizeandSyncFrequency/0004.png?featherlight=false&width=90pc)

{{% notice note %}}
Synchronization after each block significantly reduces the performance of the file system. Optimal performance is achieved by synchronizing after each file.
{{% /notice %}}