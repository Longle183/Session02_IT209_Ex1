# Bài 1: Khởi tạo Droplet trên DigitalOcean

## 1. Mục tiêu

Thực hành khởi tạo một máy chủ Droplet trên DigitalOcean sử dụng hệ điều hành Ubuntu Server, lựa chọn cấu hình phần cứng tối giản và thiết lập xác thực bằng SSH Key.

Sau khi hoàn thành, thực hiện kết nối từ máy tính cá nhân tới Droplet thông qua SSH bằng tài khoản `root` mà không cần nhập mật khẩu.

---

## 2. Yêu cầu môi trường

- Cloud Provider: DigitalOcean
- Operating System: Ubuntu 22.04 LTS
- Region: Singapore
- Droplet Type: Basic
- CPU: Shared CPU
- Storage: Regular SSD
- Authentication: SSH Key
- User: `root`

---

## 3. Tạo SSH Key

Trên máy tính cá nhân sử dụng Windows PowerShell, thực hiện lệnh:

```powershell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

SSH Key được tạo tại:

```text
C:\Users\acer\.ssh\id_ed25519
C:\Users\acer\.ssh\id_ed25519.pub
```

Trong đó:

- `id_ed25519` là Private Key.
- `id_ed25519.pub` là Public Key.

Public Key được kiểm tra bằng lệnh:

```powershell
Get-Content $env:USERPROFILE\.ssh\id_ed25519.pub
```

Sau đó copy toàn bộ nội dung Public Key để thêm vào tài khoản DigitalOcean.

---

## 4. Thêm SSH Key vào DigitalOcean

Trong DigitalOcean Console, truy cập phần quản lý SSH Keys và chọn thêm SSH Key.

Public Key được tạo từ máy cá nhân được thêm vào DigitalOcean với tên:

```text
Windows-PC
```

SSH Key này được sử dụng để xác thực khi tạo Droplet.

---

## 5. Tạo Droplet

Tạo Droplet mới trên DigitalOcean với cấu hình:

| Thành phần | Cấu hình |
|---|---|
| Region | Singapore |
| Image | Ubuntu 22.04 LTS |
| Plan | Basic |
| CPU | Shared CPU |
| Storage | Regular SSD |
| Authentication | SSH Key |
| SSH Key | Windows-PC |

Sau khi kiểm tra cấu hình, tiến hành tạo Droplet.

![Tạo Droplet](images/01-create-droplet.png)

---

## 6. Kiểm tra Droplet

Sau khi tạo thành công, Droplet có trạng thái:

```text
Running
```

DigitalOcean cung cấp một địa chỉ IP Public cho Droplet.

Ví dụ:

```text
IP Address: 159.xxx.xxx.xxx
```

![Droplet Running](images/02-droplet-running.png)

---

## 7. Kết nối SSH

Từ PowerShell trên máy tính cá nhân, sử dụng lệnh:

```powershell
ssh -i $env:USERPROFILE\.ssh\id_ed25519 root@<IP_ADDRESS_DROPLET>
```

Ví dụ:

```powershell
ssh -i $env:USERPROFILE\.ssh\id_ed25519 root@159.xxx.xxx.xxx
```

Lần đầu kết nối, hệ thống có thể yêu cầu xác nhận fingerprint của server:

```text
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Nhập:

```text
yes
```

Sau đó SSH Key được sử dụng để xác thực và đăng nhập vào Droplet.

---

## 8. Kiểm tra kết nối

Sau khi đăng nhập thành công, Terminal hiển thị thông tin Ubuntu Server và prompt của tài khoản `root`.

Kiểm tra tài khoản hiện tại:

```bash
whoami
```

Kết quả:

```text
root
```

Kiểm tra phiên bản Ubuntu:

```bash
lsb_release -a
```

Ví dụ kết quả:

```text
Distributor ID: Ubuntu
Description: Ubuntu 22.04.x LTS
Release: 22.04
Codename: jammy
```

![SSH thành công](images/03-ssh-success.png)

---

## 9. Kết quả

Đã hoàn thành việc:

- Tạo SSH Keypair trên máy tính cá nhân.
- Thêm Public Key vào DigitalOcean.
- Khởi tạo Droplet sử dụng Ubuntu 22.04 LTS.
- Chọn Region Singapore.
- Sử dụng Basic Plan với Shared CPU và Regular SSD.
- Cấu hình xác thực bằng SSH Key.
- Kết nối thành công tới Droplet bằng SSH.
- Đăng nhập thành công với tài khoản `root`.
- Kiểm tra thông tin Ubuntu Server trên Droplet.

## 10. Cấu trúc thư mục

```text
ex1/
├── README.md
└── images/
    ├── 01-create-droplet.png
    ├── 02-droplet-running.png
    └── 03-ssh-success.png
```

> Lưu ý: Không đưa Private Key (`id_ed25519`) lên GitHub.