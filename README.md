# Bài 1: Khởi tạo Droplet trên DigitalOcean

## Mục tiêu
- Thực hành đăng ký tài khoản, lựa chọn cấu hình phần cứng phù hợp và khởi tạo thành công Droplet chạy hệ điều hành Ubuntu Server trên hạ tầng đám mây DigitalOcean.
- Cấu hình xác thực an toàn bằng cặp khóa SSH (SSH Keypair) thay vì mật khẩu thô và thực hiện kết nối thành công từ máy cá nhân.

## Các bước thực hiện

### Bước 1: Tạo khóa SSH trên máy cá nhân
Sử dụng lệnh sau để tạo một cặp khóa SSH (SSH Keypair):
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Mở file chứa khóa công khai (Public Key) mặc định tại `~/.ssh/id_ed25519.pub` và copy toàn bộ nội dung trong file này.

### Bước 2: Khởi tạo Droplet trên DigitalOcean
1. Đăng nhập vào giao diện DigitalOcean Console.
2. Nhấn nút **Create** và chọn **Droplets**.
3. **Region**: Chọn datacenter **Singapore** (vị trí gần Việt Nam nhất để tối ưu tốc độ).
4. **Choose an image**: Chọn **Ubuntu** bản **22.04 LTS** (hoặc mới nhất).
5. **Choose Size**:
   - Chọn **Shared CPU**.
   - Plan: **Basic**.
   - Cấu hình: Chọn loại rẻ nhất (thường là tuỳ chọn Regular SSD $4/mo hoặc $6/mo).
6. **Authentication**: 
   - Chọn phương thức **SSH Keys**. 
   - Nhấn **New SSH Key**, dán toàn bộ nội dung Public Key đã copy ở Bước 1 vào ô trống và đặt tên cho khóa.
7. Cuộn xuống cuối trang và nhấn **Create Droplet**.

### Bước 3: Kết nối SSH tới Droplet
Sau khi Droplet được tạo xong, DigitalOcean sẽ hiển thị địa chỉ IP Public của Droplet.
Mở Terminal trên máy tính cá nhân và thực thi lệnh kết nối SSH:
```bash
ssh -i /path/to/private_key root@<IP_ADDRESS_DROPLET>
```

*(Lưu ý: Thay `/path/to/private_key` bằng đường dẫn thực tế đến file khóa bí mật (Private Key) của bạn, thông thường là `~/.ssh/id_ed25519`, và thay `<IP_ADDRESS_DROPLET>` bằng địa chỉ IP của Droplet).*

## Kết quả đạt được
- Truy cập thành công vào giao diện dòng lệnh (Terminal) của Ubuntu Server với quyền người dùng `root`.
- Không bị yêu cầu nhập mật khẩu (do đã xác thực thành công qua SSH Key).

---
**Minh chứng kết quả:**

*(Học viên chèn ảnh chụp màn hình giao diện quản lý Droplet chứa địa chỉ IP trên DigitalOcean Console hoặc ảnh chụp đoạn log đăng nhập SSH thành công trên Terminal vào bên dưới)*

![Ảnh chụp minh chứng]()
