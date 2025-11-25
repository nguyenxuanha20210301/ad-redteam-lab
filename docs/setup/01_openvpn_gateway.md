# OpenVPN Access Server Setup Guide

## 1. Hardware Specifications
- **OS:** Ubuntu Server (64-bit).
- **Role:** Đóng vai trò là VPN Gateway và Router trung chuyển giữa các vùng mạng.
- **Network Adapters:**
  - **Adapter 1 (NAT):** Để chế độ DHCP (Để máy ảo kết nối được ra Internet tải gói tin).
  - **Adapter 2 (LAN Segment: OUTSIDE):** Cấu hình IP Tĩnh (Static IP) để làm Gateway cho vùng DMZ.

## 2. Network Configuration
### Interfaces Setup
- **eth0 (NAT):**
  - IP: (nhận tự động từ VMware).
- **eth1 (LAN Segment - OUTSIDE):**
  - IP Address: `192.168.100.199`
  - Subnet: `/24` 
  - Gateway: **[ĐỂ TRỐNG]** (chính nó là Gateway).

### System Configuration
- **IP Forwarding:**  **BẬT** để cho phép gói tin đi xuyên qua server.
  - Lệnh kiểm tra: `cat /proc/sys/net/ipv4/ip_forward` (trả về 1).
  - Lệnh bật tạm thời: `sysctl -w net.ipv4.ip_forward=1`.

## 3. OpenVPN Settings (Web Admin)
- Cài Access Server trên `openvpn.net`
- Truy cập vào trang quản trị tại: `https://<IP_NAT_CỦA_UBUNTU>:943/admin`

### Add User
- Thêm người dùng **kali-attacker**
- Chọn **autologin**
- Chọn IP tĩnh, điền IP tĩnh: 172.16.11.11

### Network Settings (Phân chia dải IP)
Để tránh xung đột IP và dành riêng một dải IP đẹp cho Red Team:
- **Dynamic VPN Pool:** `172.16.10.0/24`
- **Static VPN Pool (Cho Hacker/Red Team):** `172.16.11.0/24`

### Routing Configuration (Định tuyến)
Cấu hình để máy Kali nhìn thấy vùng mạng Outside (`192.168.100.x`):
- **Should VPN clients have access to private subnets:** **YES**.
- **Subnets:** Điền dải mạng `192.168.100.0/24`.
- **Reachable via:** Chọn chế độ **ROUTE**.
  - *Lưu ý:* Chế độ Route yêu cầu `MS01` phải có lệnh `route add` thủ công để biết đường trả lời lại.