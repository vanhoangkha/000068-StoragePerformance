---
title: "Introduction"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: "<b>1. </b>"
---

#### Introduction

In this lab, we will explore best practices in pattern design, focusing on optimizing performance for both Amazon S3 and Amazon EFS.

![CloudFormation Template](/images/1-Intro/0001.png?featherlight=false&width=40pc)

#### S3 Storage Performance

Applications can achieve thousands of transactions per second when uploading and retrieving storage from Amazon S3. S3 automatically scales to high request rates. For instance, applications can reach at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second for each partitioned prefix in a bucket, with no limit on the number of prefixes. Increasing read or write performance is possible through parallelization. For example, creating 10 prefixes in a bucket can scale read performance to 55,000 requests per second. Data lake applications on S3, dealing with large-scale data, can maximize network interface usage of their Amazon EC2 instances, reaching up to 100 Gb/s on a single instance and aggregating throughput across multiple instances for even higher rates. 

Latency-sensitive applications, like social media messaging, can achieve approximately 100–200 milliseconds for small object latencies. For different architectural needs, AWS services like Amazon CloudFront or Amazon ElastiCache can accelerate performance. Amazon S3 Transfer Acceleration, using CloudFront's edge locations, offers fast, secure file transfers over long distances. Be aware of AWS KMS Limits for server-side encryption request rates.

For detailed best practices and design patterns for optimizing Amazon S3 performance, refer to the Performance Guidelines for Amazon S3 and Performance Design Patterns for Amazon S3.

#### EFS Storage Performance

Amazon EFS provides a serverless, elastic file system accessible from various AWS services and on-premises. It delivers over 10 gibibytes per second (GiBps) of throughput, 500,000 IOPS, and maintains sub-millisecond or low single-digit millisecond latencies.

#### Performance Summary

File system performance in Amazon EFS is measured by latency, throughput, and IOPS, influenced by the file system's configuration:

- Storage class – EFS One Zone or EFS Standard
- Performance mode – General Purpose or Max I/O
- Throughput mode – Bursting or Provisioned

#### Storage Classes and Performance

EFS uses two storage class types:

- EFS One Zone storage classes, including EFS One Zone and EFS One Zone-Infrequent Access (EFS One Zone-IA), replicate data within a single Availability Zone.
- EFS Standard storage classes, including EFS Standard and EFS Standard-IA, replicate data across multiple Availability Zones (Multi-AZ).

IA storage classes have higher first-byte latency compared to EFS Standard or EFS One Zone classes.

#### Performance Modes

EFS offers two performance modes:

- General Purpose mode, supporting up to 35,000 IOPS with the lowest per-operation latency, is always used with EFS One Zone storage classes and is the default for EFS Standard classes.
- Max I/O mode, supporting over 500,000 IOPS, has higher per-operation latencies compared to General Purpose mode.
