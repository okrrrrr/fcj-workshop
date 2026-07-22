---
title : "Cấu hình Nginx Reverse Proxy"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.5.4 </b> "
---

### Giới thiệu
- Trong phần này, bạn sẽ cài đặt và cấu hình Nginx trên Bastion Host để hoạt động như một Reverse Proxy. Nginx sẽ tiếp nhận các yêu cầu từ AWS Lambda và chuyển tiếp đến Flask API đang chạy trên EC2 trong Private Subnet. Việc sử dụng Reverse Proxy giúp bảo vệ máy chủ AI khỏi việc truy cập trực tiếp từ Internet, đồng thời tăng cường tính bảo mật và khả năng quản lý hệ thống.

### Các bước thực hiện

+ Cài đặt Nginx:
    + Đầu tiên cập nhật danh sách phần mềm bằng lệnh **sudo apt update**
    + Sau đó dùng lệnh **sudo apt install nginx -y**
+ Kiểm tra trạng thái của Nginx nếu thấy active(running) thì đã cài thành công
![alt text](image.png) 

### Cấu hình Reverse Proxy

- Dùng lệnh **sudo nano /etc/nginx/sites-available/default** để mở cấu hình

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://10.0.1.xxx:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```
- kiểm tra cấu hình
![alt text](image-1.png)

- Sau khi sửa lại cấu hình dùng lệnh **sudo systemctl restart nginx** để khởi động lại cấu hình

- Kiểm tra trạng thái cấu hình
![alt text](image.png) 

### Kiểm tra reverse proxy

- Dùng lệnh **curl http://localhost** thấy thông AI sandbox đang chạy là thành công
![alt text](image-2.png)






