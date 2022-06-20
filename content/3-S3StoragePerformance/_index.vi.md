---
title : "Hiệu suất lưu trữ S3"
date :  "`r Sys.Date()`" 
weight : 3
chapter : false
pre : " <b> 3. </b> "
---

#### Hiệu suất Lưu trữ **Amazon S3**

Các ứng dụng của bạn có thể dễ dàng đạt được hàng nghìn giao dịch mỗi giây theo yêu cầu hiệu suất khi tải lên và truy xuất bộ nhớ từ **Amazon S3**. **Amazon S3** tự động điều chỉnh tỷ lệ yêu cầu cao. Ví dụ: ứng dụng của bạn có thể đạt được ít nhất 3.500 PUT / COPY / POST / DELETE hoặc 5.500 yêu cầu GET / HEAD mỗi giây cho mỗi tiền tố được phân vùng . Không có giới hạn nào đối với số lượng tiền tố trong một bucket. Bạn có thể tăng hiệu suất đọc hoặc ghi của mình bằng cách sử dụng song song. Ví dụ: nếu bạn tạo 10 tiền tố trong bucket **Amazon S3** để song song hóa các lần đọc, bạn có thể mở rộng hiệu suất đọc của mình lên 55.000 yêu cầu đọc mỗi giây. Tương tự, bạn có thể chia tỷ lệ các hoạt động ghi bằng cách ghi vào nhiều tiền tố. Để biết thêm thông tin về cách tạo và sử dụng tiền tố, hãy xemTổ chức các **object** bằng cách sử dụng tiền tố .

Một số ứng dụng hồ dữ liệu trên **Amazon S3** quét hàng triệu hoặc hàng tỷ **object** cho các truy vấn chạy trên petabyte dữ liệu. Các ứng dụng hồ dữ liệu này đạt được tốc độ truyền của từng phiên bản giúp tối đa hóa việc sử dụng giao diện mạng cho **Amazon EC2 instance** của chúng , có thể lên đến 100 Gb / giây trên một phiên bản duy nhất. Sau đó, các ứng dụng này tổng hợp thông lượng qua nhiều phiên bản để có được nhiều terabit mỗi giây.

Các ứng dụng khác nhạy cảm với độ trễ, chẳng hạn như các ứng dụng nhắn tin trên mạng xã hội. Các ứng dụng này có thể đạt được độ trễ **object** nhỏ nhất quán (và độ trễ xuất byte đầu tiên đối với các **object** lớn hơn) khoảng 100–200 mili giây.

Các dịch vụ AWS khác cũng có thể giúp tăng tốc hiệu suất cho các kiến ​​trúc ứng dụng khác nhau. Ví dụ: nếu bạn muốn tốc độ truyền cao hơn qua một kết nối HTTP đơn lẻ hoặc độ trễ mili giây một chữ số, hãy sử dụng**Amazon CloudFront** hoặc Amazon ElastiCache để lưu vào bộ nhớ đệm với **Amazon S3**.

Ngoài ra, nếu bạn muốn truyền dữ liệu nhanh trong khoảng cách xa giữa máy khách và **S3 bucket**, hãy sử dụng Định cấu hình truyền tệp nhanh, an toàn bằng **Amazon S3** Transfer Acceleration . Tăng tốc truyền sử dụng các vị trí biên được phân phối toàn cầu trong CloudFront để tăng tốc quá trình vận chuyển dữ liệu qua các khoảng cách địa lý. Nếu khối lượng công việc **Amazon S3** của bạn sử dụng mã hóa phía máy chủ với Dịch vụ quản lý khóa AWS (SSE-KMS).


![CloudFormation Template](/images/1-Intro/0002.png?featherlight=false&width=10pc)

#### Nội dung

1. [S3 - Tối ưu hóa thông lượng](3.1-optimizethroughput/)
2. [S3 - Lệnh đồng bộ hóa](3.2-synccommand/)
3. [S3 - Tối ưu hóa hoạt động tệp nhỏ](3.3-optimizesmallfileoperations/)
4. [S3 - Tối ưu hóa hoạt động sao chép](3.4-optimizecopyoperations/)