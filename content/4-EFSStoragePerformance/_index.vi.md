---
title : "Hiệu suất lưu trữ EFS"
date: 2024-01-01
weight : 4 
chapter : false
pre : " <b> 4. </b> "
---

#### Hiệu suất lưu trữ **Amazon EFS**

**Amazon EFS** cung cấp hệ thống tệp đàn hồi không máy chủ, thiết lập và quên mà bạn có thể truy cập từ bất kỳ dịch vụ  compute nào trong AWS và tại chỗ, bao gồm:

- Amazon Elastic Compute Cloud (Amazon EC2)

- Amazon Elastic Container Service (Amazon ECS)

- Dịch vụ Amazon Elastic Kubernetes (Amazon EKS)

- AWS Fargate

- AWS Lambda

**Amazon EFS** cung cấp hơn 10 gibibyte mỗi giây (GiBps) thông lượng trên 500.000 IOPS và độ trễ dưới mili giây hoặc mili giây một chữ số thấp.

Hiệu suất hệ thống tệp thường được đo bằng cách sử dụng các thứ nguyên của độ trễ, thông lượng và hoạt động I / O mỗi giây (IOPS). Hiệu suất **Amazon EFS** trên các kích thước này phụ thuộc vào cấu hình hệ thống tệp của bạn. Các cấu hình sau ảnh hưởng đến hiệu suất của hệ thống tệp **Amazon EFS**:

- Lớp lưu trữ - EFS One Zone hoặc EFS Standard

- Chế độ hiệu suất - **General Purpose** hoặc I / O tối đa

- Chế độ thông lượng - Bùng nổ hoặc Cấp phép

**Các lớp lưu trữ và hiệu suất**

**Amazon EFS** sử dụng hai loại lớp lưu trữ:

- **EFS One Zone storage classes** - EFS One Zone và EFS One Zone-Truy cập không thường xuyên (EFS One Zone-IA). **EFS One Zone storage classes** sao chép dữ liệu trong một AZ duy nhất.

- **EFS Standard storage classes** - Tiêu chuẩn EFS và Tiêu chuẩn EFS-IA. **EFS Standard storage classes** sao chép dữ liệu trên nhiều AZ (Đa AZ).

- Độ trễ byte đầu tiên khi đọc từ hoặc ghi vào một trong các lớp lưu trữ IA cao hơn so với các lớp lưu trữ EFS Standard hoặc EFS One Zone.

**Chế độ hiệu suất**

**Amazon EFS** cung cấp hai chế độ hiệu suất, **General Purpose** và I / O tối đa:

- Chế độ **General Purpose** hỗ trợ lên đến 35.000 IOPS và có độ trễ cho mỗi thao tác thấp nhất. Hệ thống tệp với **EFS One Zone storage classes** luôn sử dụng chế độ hiệu suất **General Purpose**. Đối với hệ thống tệp có lớp lưu trữ Tiêu chuẩn EFS, bạn có thể sử dụng chế độ hiệu suất **General Purpose** mặc định hoặc chế độ hiệu suất I / O tối đa.

- Chế độ I / O tối đa hỗ trợ hơn 500.000 IOPS và có độ trễ trên mỗi thao tác cao hơn khi so sánh với chế độ **General Purpose**.

![CloudFormation Template](/images/1-Intro/0003.png?featherlight=false&width=10pc)

#### Nội dung

1. [EFS - Tối ưu hóa IOPS](4.1-optimizeiops/)
2. [EFS - Kích thước I / O và Tần số đồng bộ hóa](4.2-syncfrequency/)
3. [EFS - Đa luồng](4.3-multithreaded/)
4. [So sánh các giao thức truyền tệp phổ biến](4.4-fileprotocolsmodule/)



