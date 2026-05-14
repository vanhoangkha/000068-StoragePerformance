---
title : "Optimizing IOPS"
date: 2024-01-01
weight : 1
chapter : false
pre : " <b> 4.1 </b> "
---

#### Optimize EFS IOPS with multiple threads


{{% notice info %}}
This Lab will present 1,024 different file generation methods and compare the performance of each method.
{{% /notice %}}


1. In the CLI, run the following command to create 1,024 non-byte files. Record the time to complete.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")
mkdir -p /efs/tutorial/touch/${directory}
time for i in {1..1024}; do
touch /efs/tutorial/touch/${directory}/test-1.3-$i;
done;
```

![CloudFormation Template](/images/7-OptimizeIOPS/0001.png?featherlight=false&width=90pc)

2. In CLI, run the following command to create 1,024 zero byte files using multiple threads. Record the time to complete.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")
mkdir -p /efs/tutorial/touch/${directory}
time seq 1 1024 | parallel --will-cite -j 128 touch /efs/tutorial/touch/${directory}/test-1.4-{}
```

![CloudFormation Template](/images/7-OptimizeIOPS/0002.png?featherlight=false&width=90pc)

3. In the CLI, run the following command to create 1,024 non-byte files in multiple directories using multiple streams. Record the time to complete.

```
directory=$(echo $(uuidgen)| grep -o ".\\{6\\}$")
mkdir -p /efs/tutorial/touch/${directory}/{1..32}
time seq 1 32 | parallel --will-cite -j 32 touch /efs/tutorial/touch/${directory}/{}/test1.5{1..32}
```

![CloudFormation Template](/images/7-OptimizeIOPS/0003.png?featherlight=false&width=90pc)

4. Access to **Elastic File System**

   - Select **File systems**
   - Select **SID-efs**

![CloudFormation Template](/images/7-OptimizeIOPS/0004.png?featherlight=false&width=90pc)

5. The best way to take advantage of **Amazon EFS**'s distributed data storage design is to use multiple threads and inodes in parallel.

![CloudFormation Template](/images/7-OptimizeIOPS/0005.png?featherlight=false&width=90pc)