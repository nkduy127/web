---
title: 'Tổng quan về Hệ thống phân tán'
date: '2025-04-29'
categories:
  - 'distributed-systems'
  - 'network'
coverImage: '/images/anh1.jpg'
coverWidth: 16
coverHeight: 9
excerpt: Giới thiệu tổng quan, ứng dụng, khái niệm chính và kiến trúc hệ thống phân tán.
---

## 1. Hệ thống phân tán là gì?

Hệ thống phân tán là tập hợp nhiều máy tính độc lập, phối hợp với nhau để hoạt động như một hệ thống thống nhất. Chúng giao tiếp qua mạng, chia sẻ tài nguyên và phân phối công việc.
Đặc điểm:

- Mỗi thành phần có thể độc lập và chạy trên nhiều nền tảng khác nhau.

- Giao tiếp qua mạng, thường là TCP/IP.

- Khách hàng (user) thường không nhận biết rõ hệ thống đang được phân tán.

---

## 2. Các ứng dụng của hệ thống phân tán

- Dịch vụ web (Google, Facebook, Amazon)
- Hệ thống lưu trữ dữ liệu lớn (Hadoop, Cassandra, GFS)
- Ứng dụng ngân hàng, thương mại điện tử
- Hệ thống IoT, cảm biến phân tán
- Blockchain và các ứng dụng phi tập trung (DeFi, NFT)

---

## 3. Các khái niệm chính của hệ thống phân tán

### Giải thích các thuật ngữ:

- **Scalability**: Khả năng mở rộng hệ thống bằng cách thêm tài nguyên.
- **Fault Tolerance**: Khả năng tiếp tục hoạt động khi một phần hệ thống bị lỗi.
- **Availability**: Mức độ hệ thống luôn sẵn sàng phục vụ người dùng.
- **Transparency**: Người dùng không cần biết tài nguyên ở đâu hoặc hệ thống có bao nhiêu nút.
- **Concurrency**: Nhiều tiến trình chạy đồng thời một cách hiệu quả.
- **Parallelism**: Thực thi nhiều tác vụ đồng thời để tăng tốc độ xử lý.
- **Openness**: Hệ thống dễ mở rộng, tương tác với hệ thống khác.
- **Vertical Scaling**: Nâng cấp phần cứng của một nút đơn lẻ.
- **Horizontal Scaling**: Thêm nhiều nút mới vào hệ thống.
- **Load Balancer**: Bộ cân bằng tải giúp phân phối yêu cầu đều trên các nút.
- **Replication**: Sao chép dữ liệu trên nhiều nút để tăng độ tin cậy.

### Ví dụ minh họa:

- Hệ thống lưu trữ của Google sử dụng **Replication** để đảm bảo dữ liệu không mất khi một máy chủ bị lỗi.
- Facebook sử dụng **Load Balancer** để phân phối truy cập người dùng đến các máy chủ khác nhau.
- Hadoop hỗ trợ **Horizontal Scaling**: bạn có thể thêm nhiều máy chủ để xử lý dữ liệu lớn.

---

## 4. Kiến trúc của hệ thống phân tán

### 4.1. Tham khảo mô hình kiến trúc phổ biến:

- **Client-Server**
- **Three-tier Architecture**
- **Microservices Architecture**
- **Peer-to-peer (P2P)**
- **Service-Oriented Architecture (SOA)**

### 4.2. Ví dụ cụ thể:

- **Microservices**: Netflix chia ứng dụng thành các dịch vụ nhỏ (user, recommendation, streaming...) để dễ bảo trì và mở rộng.
- **P2P**: Giao thức BitTorrent không có máy chủ trung tâm, các máy người dùng chia sẻ dữ liệu trực tiếp.
