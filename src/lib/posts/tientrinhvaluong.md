---
title: 'Tiến trình và luồng'
date: '2025-04-29'
categories:
  - 'Nguyễn Khánh Duy'
  - '22010361'
coverImage: '/images/anh4.jpg'
coverWidth: 16
coverHeight: 9
---

## 1. Giới thiệu về Lenovo Legion 5

![alt text](../../../images/anh6.jpg)
![alt text](../../../images/GPU.jpg)
![alt text](../../../images/Memory.jpg)

1. CPU (Bộ xử lý trung tâm)
   Tên CPU: AMD Ryzen 5 4600H with Radeon Graphics

Số nhân / luồng: 6 cores / 12 threads

Xung nhịp cơ bản: 3.00 GHz

Xung hiện tại: ~1.5 GHz (biến động tùy tải)

Sử dụng hiện tại: Khoảng 3–6%

Nhận xét:
→ Đây là CPU hiệu năng trung bình-khá, phù hợp cho lập trình, chơi game nhẹ–trung bình, xử lý đồ họa cơ bản và học máy ở mức cơ bản.

2. RAM (Bộ nhớ truy cập ngẫu nhiên)
   Dung lượng tổng: 8.0 GB

Đang dùng: ~4.6 GB (~62%)

Tốc độ RAM: 3200 MT/s

Nhận xét:
→ Dung lượng 8GB đủ dùng cho các tác vụ văn phòng, học tập, lập trình và chạy vài máy ảo nhẹ. Nếu bạn dùng các phần mềm như Android Studio, Docker hoặc nhiều tab trình duyệt, bạn sẽ cảm thấy thiếu RAM.

3. GPU (Card đồ họa rời)
   Tên: NVIDIA GeForce GTX 1650 Ti

Bộ nhớ GPU: 4.0 GB

Sử dụng hiện tại: 0%

Nhiệt độ: 45°C

Nhận xét:
→ Đây là GPU tầm trung. Rất tốt cho học tập, dựng video nhẹ, chơi game phổ thông và xử lý song song (có thể dùng CUDA cho học máy ở mức entry-level).

Tổng kết hiệu năng máy:
Máy bạn có cấu hình khá ổn để học CNTT, lập trình, sử dụng phần mềm phát triển, máy ảo nhẹ và các tác vụ kỹ thuật thông thường.

Nếu bạn định học sâu về AI/học máy hoặc làm đồ họa nặng (3D, dựng phim), nên cân nhắc nâng RAM lên 16GB và dùng GPU mạnh hơn.

## 2. Liệt kê ít nhất 12 bài toán trong CNTT dùng đa luồng / đa tiến trình

Web Server xử lý nhiều yêu cầu đồng thời: mỗi yêu cầu từ người dùng được xử lý bằng một luồng hoặc tiến trình riêng biệt để tăng khả năng phục vụ đồng thời.

Tải nhiều tệp cùng lúc (multi-download): mỗi tệp được tải xuống bằng một luồng khác nhau để rút ngắn tổng thời gian chờ.

Trình duyệt web (như Chrome): sử dụng đa tiến trình, mỗi tab hoạt động như một tiến trình riêng biệt để tránh treo toàn bộ trình duyệt khi một tab gặp lỗi.

Trò chơi điện tử (Game engine): sử dụng đa luồng để tách riêng các phần như xử lý hình ảnh, âm thanh, mạng, và AI nhằm tăng hiệu năng.

Xử lý ảnh hoặc video (rendering, chuyển định dạng): chia nhỏ dữ liệu và xử lý song song bằng nhiều luồng để đẩy nhanh tốc độ xử lý.

Phân tích dữ liệu lớn (Big Data): sử dụng nhiều tiến trình hoặc hệ thống phân tán để xử lý dữ liệu trên nhiều lõi CPU hoặc nhiều máy tính.

Biên dịch chương trình lớn (compile project): mỗi tệp mã nguồn có thể được biên dịch bởi một tiến trình độc lập để rút ngắn thời gian build.

Phần mềm diệt virus quét toàn bộ hệ thống: chia từng ổ đĩa, thư mục, hoặc tệp thành các tác vụ riêng xử lý song song.

Phát nhạc hoặc xem video trực tuyến: sử dụng đa luồng để vừa tải dữ liệu, vừa giải mã và hiển thị đồng thời.

Ứng dụng mạng xã hội (xử lý feed, tin nhắn, upload ảnh): nhiều luồng thực hiện các chức năng khác nhau để đảm bảo tốc độ và độ phản hồi.

Máy ảo (Virtual Machine) hoặc giả lập hệ điều hành: mỗi hệ điều hành giả lập chạy như một tiến trình độc lập.

Huấn luyện mô hình AI, học sâu (Deep Learning): sử dụng cả đa luồng, đa tiến trình, và hệ thống phân tán để tận dụng tối đa tài nguyên tính toán.

---

## 3. Liệt kê các trường hợp nên dùng thread, process, hoặc cả hai

![alt text](../../../images/anh5.jpg)

### 3.1 Khi nên dùng Thread:

Khi các tác vụ cần chia sẻ dữ liệu, dùng thread sẽ tiện hơn vì thread trong cùng một process có thể dùng chung bộ nhớ.

Các công việc I/O-bound như đọc ghi file, gửi nhận dữ liệu mạng, có thể sử dụng nhiều thread để tránh chặn toàn bộ chương trình.

Khi cần thực hiện các nhiệm vụ nhỏ, nhanh, nhẹ, chẳng hạn như xử lý sự kiện, cập nhật giao diện trong ứng dụng desktop.

### 3.2 Khi nên dùng Process:

Khi cần xử lý độc lập, không phụ thuộc lẫn nhau, hoặc cần cách ly về bảo mật và bộ nhớ (sandbox).

Dùng khi có thể xảy ra lỗi nặng: nếu một process bị lỗi, các process khác không bị ảnh hưởng.

Khi các tác vụ rất nặng về CPU và có thể tận dụng đa lõi CPU, thì chia thành nhiều process có thể hiệu quả hơn.

Ví dụ: Trình duyệt web (như Chrome) sử dụng mỗi tab là một process riêng để tránh ảnh hưởng lẫn nhau.

---

### 3.2 Khi nên dùng Process:

Khi nên dùng cả hai (thread + process):
Trong các hệ thống phức tạp, có thể dùng nhiều process, và mỗi process lại có nhiều thread để xử lý song song các phần việc nhỏ hơn.

Ví dụ: Một IDE như Visual Studio Code có thể dùng nhiều process cho từng extension và trong mỗi process lại có nhiều thread để xử lý giao diện, ngôn ngữ, biên dịch.

---

## 4. ChatGPT training tập dữ liệu lớn bằng Distributed System như thế nào

### 4.1 Tóm tắt quá trình training ChatGPT:

Tập dữ liệu cực lớn (tính bằng TB – petabyte) từ nhiều nguồn: sách, web, bài báo, mã nguồn...

Mô hình GPT được huấn luyện bằng kỹ thuật "Transformer" trên nhiều GPU/TPU song song.

Sử dụng Distributed Training:

Data Parallelism: Chia tập dữ liệu lớn thành nhiều phần, mỗi máy xử lý 1 phần giống nhau của mô hình.

Model Parallelism: Chia nhỏ chính mô hình để chạy trên nhiều GPU, mỗi GPU xử lý một phần mô hình.

Áp dụng Gradient Accumulation và Mixed Precision để tiết kiệm bộ nhớ và tăng tốc.

Hạ tầng dùng: GPU NVIDIA A100 hoặc TPU v4, hệ thống kết nối tốc độ cao (NVLink, Infiniband...).

### 4.2 Tài liệu tham khảo:

Microsoft ZeRO Paper

OpenAI Blog on GPT-3

DeepSpeed by Microsoft

Hugging Face: Training Large Models

---
