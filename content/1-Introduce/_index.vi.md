---
title : "Giới thiệu"
date: 2024-01-01
weight : 1 
chapter : false
pre : " <b> 1. </b> "
---

#### Giới thiệu

Trong bài lab này, chúng ta sẽ thực hiện các phương pháp hay nhất về thiết kế mẫu: tối ưu hóa hiệu suất ****Amazon S3**** và tối ưu hóa hiệu suất ****Amazon EFS****

![CloudFormation Template](/images/1-Intro/0001.png?featherlight=false&width=40pc)

#### Hiệu suất lưu trữ **Amazon S3**

Các ứng dụng của bạn có thể dễ dàng đạt được hàng nghìn giao dịch mỗi giây theo yêu cầu hiệu suất khi tải lên và truy xuất bộ nhớ từ **Amazon S3**. **Amazon S3** tự động điều chỉnh tỷ lệ yêu cầu cao. Ví dụ: ứng dụng của bạn có thể đạt được ít nhất 3.500 PUT / COPY / POST / DELETE hoặc 5.500 yêu cầu GET / HEAD mỗi giây cho mỗi tiền tố được phân vùng . Không có giới hạn nào đối với số lượng tiền tố trong một bucket. Bạn có thể tăng hiệu suất đọc hoặc ghi của mình bằng cách sử dụng song song. Ví dụ: nếu bạn tạo 10 tiền tố trong bucket **Amazon S3** để song song hóa các lần đọc, bạn có thể mở rộng hiệu suất đọc của mình lên 55.000 yêu cầu đọc mỗi giây. Tương tự, bạn có thể chia tỷ lệ các hoạt động ghi bằng cách ghi vào nhiều tiền tố. Để biết thêm thông tin về cách tạo và sử dụng tiền tố, hãy xemTổ chức các **object** bằng cách sử dụng tiền tố .

Một số ứng dụng hồ dữ liệu trên **Amazon S3** quét hàng triệu hoặc hàng tỷ **object** cho các truy vấn chạy trên petabyte dữ liệu. Các ứng dụng hồ dữ liệu này đạt được tốc độ truyền của từng phiên bản giúp tối đa hóa việc sử dụng giao diện mạng cho **Amazon EC2 instance** của chúng , có thể lên đến 100 Gb / giây trên một phiên bản duy nhất. Sau đó, các ứng dụng này tổng hợp thông lượng qua nhiều phiên bản để có được nhiều terabit mỗi giây.

Các ứng dụng khác nhạy cảm với độ trễ, chẳng hạn như các ứng dụng nhắn tin trên mạng xã hội. Các ứng dụng này có thể đạt được độ trễ **object** nhỏ nhất quán (và độ trễ xuất byte đầu tiên đối với các **object** lớn hơn) khoảng 100–200 mili giây.

Các dịch vụ AWS khác cũng có thể giúp tăng tốc hiệu suất cho các kiến ​​trúc ứng dụng khác nhau. Ví dụ: nếu bạn muốn tốc độ truyền cao hơn qua một kết nối HTTP đơn lẻ hoặc độ trễ mili giây một chữ số, hãy sử dụng**Amazon CloudFront** hoặc Amazon ElastiCache để lưu vào bộ nhớ đệm với **Amazon S3**.

Ngoài ra, nếu bạn muốn truyền dữ liệu nhanh trong khoảng cách xa giữa máy khách và **S3 bucket**, hãy sử dụng Định cấu hình truyền tệp nhanh, an toàn bằng **Amazon S3** Transfer Acceleration . Tăng tốc truyền sử dụng các vị trí biên được phân phối toàn cầu trong CloudFront để tăng tốc quá trình vận chuyển dữ liệu qua các khoảng cách địa lý. Nếu khối lượng công việc **Amazon S3** của bạn sử dụng mã hóa phía máy chủ với Dịch vụ quản lý khóa AWS (SSE-KMS)

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