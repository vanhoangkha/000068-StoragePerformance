---
title : "EFS Storage Performance"
date : "`r Sys.Date()`"
weight : 4
chapter : false
pre : " <b> 4. </b> "
---

#### Storage Performance **Amazon EFS**

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

#### Content

1. [EFS - IOPS Optimization](4.1-optimizeiops/)
2. [EFS - I/O Size and Sync Frequency](4.2-syncfrequency/)
3. [EFS - Multithreaded](4.3-multithreaded/)
4. [Compare Common File Transfer Protocols](4.4-fileprotocolsmodule/)