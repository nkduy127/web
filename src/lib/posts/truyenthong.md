---
title: 'Truyền ThôngThông'
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

```bash
docker run -d --hostname rabbit --name rabbitmq \
  -p 5672:5672 -p 15672:15672 \
  rabbitmq:3-management
```

Sau khi chạy, giao diện quản lý truy cập tại: `http://localhost:15672` (user/pass: guest/guest).

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
