---
title: "EFS Storage Performance"
date: 2024-01-01
weight: 4
chapter: false
pre: "<b>4.</b>"
---

#### Storage Performance **Amazon EFS**

Amazon EFS provides a serverless, set-and-forget elastic file system that can be accessed from various compute services within AWS and on-premises, such as:

- Amazon Elastic Compute Cloud (Amazon EC2)
- Amazon Elastic Container Service (Amazon ECS)
- Amazon Elastic Kubernetes Service (Amazon EKS)
- AWS Fargate
- AWS Lambda

Amazon EFS delivers over 10 gibibytes per second (GiBps) of throughput, more than 500,000 IOPS, and latencies that are sub-millisecond or in the low single-digit milliseconds.

#### Performance Summary

File system performance is usually measured in latency, throughput, and I/O operations per second (IOPS). The performance of an Amazon EFS file system across these metrics depends on its configuration, including:

- Storage Class: EFS One Zone or EFS Standard
- Performance Mode: General Purpose or Max I/O
- Throughput Mode: Bursting or Provisioned

#### Storage Classes and Performance

Amazon EFS utilizes two storage class types:

- **EFS One Zone Storage Classes:** EFS One Zone and EFS One Zone-Infrequent Access (EFS One Zone-IA). Data is replicated within a single Availability Zone.
- **EFS Standard Storage Classes:** EFS Standard and EFS Standard-IA. Data is replicated across multiple Availability Zones (Multi-AZ).

The first-byte latency for the IA storage classes is higher compared to the EFS Standard or EFS One Zone classes.

#### Performance Modes

Amazon EFS offers two performance modes: General Purpose and Max I/O:

- **General Purpose Mode:** Supports up to 35,000 IOPS with the lowest per-operation latency. File systems with EFS One Zone storage classes always operate in General Purpose mode. For EFS Standard storage classes, you can choose between General Purpose (default) and Max I/O modes.
- **Max I/O Mode:** Supports over 500,000 IOPS with higher per-operation latencies compared to General Purpose mode.

#### Content

1. [EFS - IOPS Optimization](4.1-optimizeiops/)
2. [EFS - I/O Size and Sync Frequency](4.2-syncfrequency/)
3. [EFS - Multithreaded](4.3-multithreaded/)
4. [Compare Common File Transfer Protocols](4.4-fileprotocolsmodule/)
