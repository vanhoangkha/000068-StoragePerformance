---
title : "File Protocol Module"
date: 2024-01-01
weight : 4
chapter : false
pre : " <b> 4.4 </b> "
---

#### Compare popular file transfer protocols

{{% notice info %}}
This Lab will compare the performance of different file transfer utilities and EFS.
{{% /notice %}}

1. In the CLI, run the following commands to verify the EC2 instance has approximately 2GB of EBS volume.

```
du -csh /ebs/tutorial/data-1m/
```


![CloudFormation Template](/images/10-Underconstruction/0001.png?featherlight=false&width=90pc)

2. Run the following commands to verify the EC2 instance has 2000 files in the EBS volume.

```
find /ebs/tutorial/data-1m/. -type f | wc -l
```


![CloudFormation Template](/images/10-Underconstruction/0002.png?featherlight=false&width=90pc)

3. Run the following commands to transfer files from EBS to EFS using rsync. Record the completion time. The command will take a few minutes to complete, don't worry if it hangs.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time rsync -r /ebs/tutorial/data-1m/ /efs/tutorial/rsync/
```


![CloudFormation Template](/images/10-Underconstruction/0003.png?featherlight=false&width=90pc)

4. Run the following commands to transfer files from EBS to EFS using the copy command. Record the completion time. The command will take a few minutes to complete, don't worry if it hangs.


```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time cp -r /ebs/tutorial/data-1m/* /efs/tutorial/cp/
```


![CloudFormation Template](/images/10-Underconstruction/0004.png?featherlight=false&width=90pc)

5. Run the following commands to set the $thread variable to 4 threads per CPU.

```
threads=$(($(nproc --all) * 4))
echo $threads
```


![CloudFormation Template](/images/10-Underconstruction/0005.png?featherlight=false&width=90pc)

6. Run the following commands to transfer files from EBS to EFS using fpsync. Record the completion time. The command will take a few minutes to complete.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time fpsync -n ${threads} -v /ebs/tutorial/data-1m/ /efs/tutorial/fpsync/
```


![CloudFormation Template](/images/10-Underconstruction/0006.png?featherlight=false&width=90pc)

7. Run the following commands to transfer files from EBS to EFS using cp + GNU Parallel. Record the completion time. The command will take a few minutes to complete.

```
sudo su
sync && echo 3 > /proc/sys/vm/drop_caches
exit
time find /ebs/tutorial/data-1m/. -type f | parallel --will-cite -j ${threads} cp {} /efs/tutorial/parallelcp
```

![CloudFormation Template](/images/10-Underconstruction/0007.png?featherlight=false&width=90pc)


{{% notice note %}}
Not all file transfer utilities work the same. The file system is distributed over an unlimited number of storage servers, and this distributed data storage design means that multithreaded applications such as fpsync, mcp, and GNU in parallel can leverage throughput levels. significant amount and IOPS to EFS when compared to single-threaded applications.
{{% /notice %}}