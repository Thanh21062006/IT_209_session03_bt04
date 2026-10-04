# Bài 4: Chạy song song nhiều cổng dịch vụ (Nginx Virtual Hosts)

### 1. Tạo thư mục mã nguồn cho 2 trang web
Tạo thư mục và file cấu hình cho Beta App và Internal App:
```bash
sudo mkdir -p /var/www/beta-app/html/
sudo mkdir -p /var/www/internal-app/html/
```
*(Các file `index.html` của beta-app và internal-app đã được đính kèm theo repository).*

### 2. Cấu hình Nginx Virtual Hosts
Cấu hình 1 file duy nhất lắng nghe 2 cổng khác nhau:
```bash
sudo nano /etc/nginx/sites-available/multi-port.conf
```
*(Nội dung file `multi-port.conf` đã đính kèm theo repository).*

Kích hoạt và reload Nginx:
```bash
sudo ln -s /etc/nginx/sites-available/multi-port.conf /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 3. Mở cổng trên Tường lửa
Mở cổng trên OS với UFW:
```bash
sudo ufw allow 8080/tcp
sudo ufw allow 8090/tcp
```
Và cấu hình Inbound Rules cho Cloud Firewall trên DigitalOcean để mở 8080 và 8090.

### 4. Kiểm tra
*Lưu ý: Vì thẻ visa của em bị khoá nên không thể tạo droplet để chạy thử nghiệm các lệnh này.*

Kiểm tra trang Beta App:
```bash
curl http://<IP_ADDRESS_DROPLET>:8080
```
Kiểm tra trang Internal App:
```bash
curl http://<IP_ADDRESS_DROPLET>:8090
```
