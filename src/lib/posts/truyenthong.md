---
title: 'Truyền Thông'
date: '2025-04-29'
categories:
  - 'Nguyễn Khánh Duy'
  - '22010361'
coverImage: '/images/anh7.jpg'
coverWidth: 16
coverHeight: 9
# BÁO CÁO BÀI TẬP - HỆ THỐNG TRUYỀN THÔNG ĐIỆP VÀ RPC
---

## Bài tập 1: Tìm hiểu cơ chế, chức năng và cài đặt dịch vụ truyền thông điệp (RabbitMQ)

### 1. Giới thiệu về RabbitMQ:

RabbitMQ là một message broker được sử dụng rộng rãi trong các hệ thống phân tán để chuyển giao thông điệp giữa các service. Điểm mạnh của RabbitMQ là khả năng hỗ trợ nhiều giao thức như AMQP, MQTT, STOMP.

### 2. Cơ chế hoạt động:

- **Producer**: gửi thông điệp.
- **Exchange**: nhận thông điệp và quyết định gửi nó đến queue nào.
- **Queue**: nơi lưu trữ thông điệp.
- **Consumer**: nhận và xử lý thông điệp.

### 3. Các chức năng chính:

- Đồng bộ giao tiếp giữa các service.
- Làm việc với nhiều kiểu routing: direct, fanout, topic, headers.
- Bảo đảm tin nhắn không bị mất.
- Quản lý hàng đợi linh hoạt, dễ dùng.

### 4. Hướng dẫn cài đặt RabbitMQ (Docker):

## ✅ Yêu cầu trước khi bắt đầu

- Cài đặt sẵn **Docker** (Windows, macOS hoặc Linux).
- Kiểm tra Docker đã hoạt động:
```bash
docker --version
```

---

## 🔧 Bước 1: Chạy RabbitMQ với Docker

Sử dụng lệnh sau để tải và khởi động container RabbitMQ:

```bash
docker run -d \
  --name rabbitmq \
  --hostname rabbitmq-host \
  -p 5672:5672 \
  -p 15672:15672 \
  rabbitmq:3-management
```

### 📌 Giải thích các tham số:
- `--name rabbitmq`: Đặt tên cho container.
- `--hostname rabbitmq-host`: Đặt hostname trong mạng nội bộ của Docker.
- `-p 5672:5672`: Mở cổng AMQP (ứng dụng sẽ dùng cổng này để kết nối).
- `-p 15672:15672`: Mở cổng giao diện quản trị Web.
- `rabbitmq:3-management`: Image có sẵn plugin quản trị qua trình duyệt.

---

## 🌐 Bước 2: Truy cập Giao diện Quản lý RabbitMQ

- Trình duyệt truy cập: [http://localhost:15672](http://localhost:15672)
- Đăng nhập với:
  - **Username:** `guest`
  - **Password:** `guest`

> ⚠️ Lưu ý: Người dùng `guest` chỉ có thể đăng nhập từ localhost. Nếu chạy trên server từ xa, cần tạo user mới.

---

## 🔍 Bước 3: Kiểm tra container

- Kiểm tra container đang chạy:
```bash
docker ps
```

- Xem logs container RabbitMQ:
```bash
docker logs -f rabbitmq
```

---

## 🧹 Bước 4: Dừng hoặc xóa container khi cần

- Dừng container:
```bash
docker stop rabbitmq
```

- Xóa container:
```bash
docker rm rabbitmq
```

---



---

## Bài tập 2: Xây dựng hệ thống đơn giản dùng RabbitMQ

### 1. Cài đặt thư viện pika:

```bash
pip install pika
```

### 2. Producer gửi thông điệp:

```python
import pika
conn = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = conn.channel()
channel.queue_declare(queue='demo')
channel.basic_publish(exchange='', routing_key='demo', body='Xin chao!')
print("[Producer] Da gui thong diep")
conn.close()
```

### 3. Consumer nhận thông điệp:

```python
import pika
conn = pika.BlockingConnection(pika.ConnectionParameters('localhost'))
channel = conn.channel()
channel.queue_declare(queue='demo')

def xu_ly(ch, method, properties, body):
    print("[Consumer] Nhan duoc:", body.decode())

channel.basic_consume(queue='demo', on_message_callback=xu_ly, auto_ack=True)
print("[Consumer] Dang cho tin nhan...")
channel.start_consuming()
```

---

## Bài tập 3: Tìm hiểu và demo RPC dựa trên JSON

### 1. Lý do chọn JSON-RPC:

- Nhẹ nhàng hơn XMLRPC.
- Thích hợp RESTful và microservices.

### 2. Cài đặt thư viện:

```bash
pip install jsonrpclib-pelix
```

### 3. Server RPC:

```python
from jsonrpclib.SimpleJSONRPCServer import SimpleJSONRPCServer

def cong(a, b):
    return a + b

server = SimpleJSONRPCServer(('localhost', 8000))
server.register_function(cong, 'cong')
print("[RPC Server] Dang lang nghe tai cong 8000...")
server.serve_forever()
```

### 4. Client RPC:

```python
import jsonrpclib
proxy = jsonrpclib.Server('http://localhost:8000')
kq = proxy.cong(7, 5)
print("[RPC Client] Ket qua 7 + 5 =", kq)
```

---

## Kết luận:

Bài tập đã giúp em hiểu rõ về người trung gian truyền thông trong hệ thống phân tán (như RabbitMQ) và cách RPC giúp hai ứng dụng gọi-hồi giá trị trực tiếp như hàm cùng host.

Bài demo đơn giản nhưng đủ để thể hiện được ý tưởng thiết kế và triển khai các hệ thống backend linh hoạt, tự động.
