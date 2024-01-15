---
title: "Storage Performance Lab"
date: "`r Sys.Date()`"
weight: 1
chapter: false
---

# Storage Performance Lab

In this lab, we will explore best practices in pattern design, focusing on optimizing performance in **Amazon S3** and **Amazon EFS**.

![CloudFormation Template](/images/1-Intro/0001.png?featherlight=false&width=40pc)

#### S3 Storage Performance

Amazon S3 allows applications to achieve thousands of transactions per second when uploading and retrieving storage. This service scales automatically to high request rates. For instance, applications can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second for each partitioned prefix. Parallelization can further increase read or write performance. For example, creating 10 prefixes in a bucket can scale read performance to 55,000 requests per second. Write operations can be scaled similarly. For more information on using prefixes, refer to "Organizing objects using prefixes."

Data lake applications on Amazon S3, scanning millions or billions of objects over petabytes of data, can achieve high single-instance transfer rates, using up to 100 Gb/s on a single Amazon EC2 instance. These rates can be aggregated across multiple instances for even greater throughput.

Applications sensitive to latency, like social media messaging, can achieve small object latencies of approximately 100–200 milliseconds.

Other AWS services, such as Amazon CloudFront or Amazon ElastiCache, can accelerate performance for different architectures. Amazon S3 Transfer Acceleration, leveraging CloudFront's edge locations, can significantly speed up data transport over long distances. For workloads using server-side encryption with AWS Key Management Service (SSE-KMS), refer to the AWS Key Management Service Developer Guide for supported request rates.

For optimizing Amazon S3 performance, consult the Performance Guidelines for Amazon S3 and Performance Design Patterns for Amazon S3.

#### EFS Storage Performance

Amazon EFS offers a serverless, elastic file system accessible from various AWS services and on-premises. It delivers over 10 gibibytes per second (GiBps) of throughput, 500,000 IOPS, and sub-millisecond or low single-digit millisecond latencies.

#### Performance Summary

File system performance in Amazon EFS is measured by latency, throughput, and IOPS. The performance depends on the file system's configuration, influenced by:

- Storage class (EFS One Zone or EFS Standard)
- Performance mode (General Purpose or Max I/O)
- Throughput mode (Bursting or Provisioned)

#### Storage Classes and Performance

Amazon EFS uses two storage class types:

- EFS One Zone storage classes (EFS One Zone and EFS One Zone-IA) replicate data within a single Availability Zone.
- EFS Standard storage classes (EFS Standard and EFS Standard-IA) replicate data across multiple Availability Zones.

Latency for the IA classes is higher compared to the Standard or One Zone classes.

#### Performance Modes

Amazon EFS offers two performance modes:

- General Purpose mode, supporting up to 35,000 IOPS with the lowest latency.
- Max I/O mode, supporting over 500,000 IOPS with higher latency compared to General Purpose mode.

#### Content

1. [Introduction](1-introduce/)
2. [Preparation](2-prerequiste/)
3. [Storage Performance **Amazon S3**](3-s3storageperformance/)
4. [Amazon EFS Storage Performance](4-efsstorageperformance/)
5. [Resource Cleanup](5-cleanup/)
