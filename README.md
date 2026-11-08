# Storage Performance Lab

> Optimizing AWS storage performance.

A hands-on workshop from the [AWS First Cloud Journey](https://github.com/vanhoangkha/aws-first-cloud-journey) series, available in English and Vietnamese.

**Read the workshop online:** https://vanhoangkha.github.io/000068-StoragePerformance/

## Overview

In this lab, we will explore best practices in pattern design, focusing on optimizing performance in Amazon S3 and Amazon EFS.

Amazon S3 allows applications to achieve thousands of transactions per second when uploading and retrieving storage. This service scales automatically to high request rates. For instance, applications can achieve at least 3,500 PUT/COPY/POST/DELETE or 5,500 GET/HEAD requests per second for each partitioned prefix. Parallelization can further increase read or write performance. For example, creating 10 prefixes in a bucket can scale read performance to 55,000 requests per second. Write operations can be scaled similarly. For more information on using prefixes, refer to "Organizing objects using prefixes."

## Workshop contents

1. Introduction
2. Preparation
   - Launch CloudFormation Template
   - Configuring security groups
   - Connecting to EC2
3. S3 Storage Performance
   - Optimize Throughput
   - Sync command
   - S3 - Optimize Small File Operations
   - S3 - Optimize Copy Operations
4. EFS Storage Performance
   - Optimizing IOPS
   - I/O Size and Sync Frequency
   - Multi-threading
   - File Protocol Module
5. Clean up resources

## Prerequisites

- An AWS account with permissions to create the resources used in the labs
- Basic familiarity with the AWS Management Console
- [Hugo](https://gohugo.io/installation/) (extended edition) if you want to run the site locally

## Run locally

```bash
git clone --recurse-submodules https://github.com/vanhoangkha/000068-StoragePerformance.git
cd 000068-StoragePerformance
hugo server
```

Then open http://localhost:1313 in your browser.

## Repository structure

| Path | Purpose |
| --- | --- |
| `content/` | Workshop pages (`*.md` English, `*.vi.md` Vietnamese) |
| `static/` | Images and other static assets |
| `layouts/` | Hugo layout overrides |
| `themes/` | Hugo theme |
| `config.toml` | Site configuration |

## Cost and cleanup

The labs create AWS resources that may incur charges. Complete the **Clean up** chapter when you finish to remove them.

## Contributing

Contributions are welcome. See [CONTRIBUTING.md](CONTRIBUTING.md).

To report a security issue, see [SECURITY.md](SECURITY.md).

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).
