# MS01 (Bastion Host) Setup Guide

## 1. Virtual Machine Specifications
- **Hostname:** MS01
- **Operating System:** Windows Server 2019 Datacenter.
- **CPU:** 2 vCPUs.
- **RAM:** 4 GB.
- **Hard Disk:** 60 GB.
- **Network Adapters:**
  - **Network Adapter 1:** Kết nối vào LAN Segment tên là `corp-outside`.
  - **Network Adapter 2:** Kết nối vào LAN Segment tên là `corp-inside`.

## 2. Network Configuration

### Adapter 1: OUTSIDE Interface (Facing OpenVPN)
Card mạng này kết nối với vùng DMZ/Outside và giao tiếp trực tiếp với VPN Gateway.

- **IP Address:** `192.168.100.201`
- **Subnet Mask:** `255.255.255.0` (/24).
- **Default Gateway:** [ĐỂ TRỐNG].
- **DNS Server:** [ĐỂ TRỐNG].

### Adapter 2: INSIDE Interface (Facing DC01)
Card mạng này kết nối vào vùng nội bộ (Intranet) để nói chuyện với Domain Controller.

- **IP Address:** `10.10.1.201`
- **Subnet Mask:** `255.255.255.0` (/24).
- **Default Gateway:** [ĐỂ TRỐNG].
- **DNS Server:** [ĐỂ TRỐNG].

## 3. Routing Configuration 
Vì MS01 đóng vai trò là Bastion Host, nó cần biết đường để trả lời lại các gói tin đến từ máy tấn công (Kali) thuộc dải mạng VPN (`172.16.11.0/24`).

**Command Prompt (quyền Admin):**
```cmd
route add 172.16.11.0 mask 255.255.255.0 192.168.100.199 metric 1 /p