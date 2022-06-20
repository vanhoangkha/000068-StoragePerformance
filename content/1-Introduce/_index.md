---
title : "Introduction"
date :  "`r Sys.Date()`" 
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Introduction

In this lab, we'll go through pattern design best practices: optimizing performance ****Amazon S3**** and optimizing performance **Amazon EFS**

![CloudFormation Template](/images/1-Intro/0001.png?featherlight=false&width=40pc)

#### S3 Storage Performance

Your applications can easily achieve thousands of transactions per second in request performance when uploading and retrieving storage from Amazon S3. Amazon S3 automatically scales to high request rates. For example, your application can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second per partitioned prefix. There are no limits to the number of prefixes in a bucket. You can increase your read or write performance by using parallelization. For example, if you create 10 prefixes in an Amazon S3 bucket to parallelize reads, you could scale your read performance to 55,000 read requests per second. Similarly, you can scale write operations by writing to multiple prefixes. For more information about creating and using prefixes, see Organizing objects using prefixes.

Some data lake applications on Amazon S3 scan millions or billions of objects for queries that run over petabytes of data. These data lake applications achieve single-instance transfer rates that maximize the network interface use for their Amazon EC2 instance, which can be up to 100 Gb/s on a single instance. These applications then aggregate throughput across multiple instances to get multiple terabits per second.

Other applications are sensitive to latency, such as social media messaging applications. These applications can achieve consistent small object latencies (and first-byte-out latencies for larger objects) of roughly 100–200 milliseconds.

Other AWS services can also help accelerate performance for different application architectures. For example, if you want higher transfer rates over a single HTTP connection or single-digit millisecond latencies, use Amazon CloudFront or Amazon ElastiCache for caching with Amazon S3.

Additionally, if you want fast data transport over long distances between a client and an S3 bucket, use Configuring fast, secure file transfers using Amazon S3 Transfer Acceleration. Transfer Acceleration uses the globally distributed edge locations in CloudFront to accelerate data transport over geographical distances. If your Amazon S3 workload uses server-side encryption with AWS Key Management Service (SSE-KMS), see AWS KMS Limits in the AWS Key Management Service Developer Guide for information about the request rates supported for your use case.

The following topics describe best practice guidelines and design patterns for optimizing performance for applications that use Amazon S3. Refer to the Performance Guidelines for Amazon S3 and Performance Design Patterns for Amazon S3 for the most current information about performance optimization for Amazon S3.

#### EFS Storage Performance

Amazon EFS provides a serverless, set-and-forget elastic file system that you can access from any compute service within AWS and on-premises, including:

- Amazon Elastic Compute Cloud (Amazon EC2)

- Amazon Elastic Container Service (Amazon ECS)

- Amazon Elastic Kubernetes Service (Amazon EKS)

- AWS Fargate

- AWS Lambda

Amazon EFS delivers more than 10 gibibytes per second (GiBps) of throughput over 500,000 IOPS, and sub-millisecond or low single digit millisecond latencies.

#### Performance summary

File system performance is typically measured using the dimensions of latency, throughput, and I/O operations per second (IOPS). Amazon EFS performance across these dimensions depends on your file system's configuration. The following configurations impact the performance of an Amazon EFS file system:

- Storage class – EFS One Zone or EFS Standard

- Performance mode – General Purpose or Max I/O

- Throughput mode – Bursting or Provisioned

#### Storage classes and performance

Amazon EFS uses two types of storage classes:

- EFS One Zone storage classes – EFS One Zone and EFS One Zone-Infrequent Access (EFS One Zone-IA). The EFS One Zone storage classes replicate data within a single Availability Zone.

- EFS Standard storage classes – EFS Standard and EFS Standard-IA. The EFS Standard storage classes replicate data across multiple Availability Zones (Multi-AZ).

First-byte latency when reading from or writing to either of the IA storage classes is higher than that for the EFS Standard or EFS One Zone storage classes.

#### Performance modes

Amazon EFS offers two performance modes, General Purpose and Max I/O:

- General Purpose mode supports up to 35,000 IOPS and has the lowest per-operation latency. File systems with EFS One Zone storage classes always use General Purpose performance mode. For file systems with EFS Standard storage classes, you can use either the default General Purpose performance mode or the Max I/O performance mode.

- Max I/O mode supports 500,000+ IOPS and has higher per-operation latencies when compared to General Purpose mode.