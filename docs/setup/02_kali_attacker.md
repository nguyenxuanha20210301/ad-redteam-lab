# Kali Linux (Attacker) Setup Guide

## 1. Virtual Machine Specifications
- **Hostname:** Kali-Attacker
- **OS:** Kali Linux (Latest Version)
- **Role:** Red Team Operations / C2 Server / Scanner
- **Network Adapter:**
  - **Adapter 1 (NAT):** (DHCP from VMware)

## 2. VPN Connection Setup
- **Software:** OpenVPN Client (`sudo apt install openvpn`)
- **Connection Profile:**
  - Download `profile-autologin.ovpn` from `https://<OPENVPN_IP>:943/`
  - Login as user: `kali-attacker`
- **Static IP Assignment:**
  - Ensure the user `kali` is assigned the Static IP **`172.16.11.11`** in the OpenVPN Admin UI.

### Connecting to the Lab
Run the following command in the directory containing your profile:
```bash
sudo openvpn profile-autologin.ovpn
```