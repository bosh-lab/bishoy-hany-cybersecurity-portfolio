# 📡 Wireless Network Design

## 🔍 Project Overview
Designed and implemented a secure wireless network topology using Cisco Packet Tracer, simulating a real-world enterprise wireless deployment.

## 🎯 Objectives
- Design a scalable wireless network architecture
- Configure wireless access points and controllers
- Implement security measures (WPA2/WPA3, SSID segmentation)
- Ensure proper IP addressing and DHCP configuration

## 🛠️ Tools Used
- **Cisco Packet Tracer** - Network simulation
- **Wireless Access Points** - Cisco Aironet (simulated)
- **Wireless LAN Controller (WLC)** - Centralized management
- **DHCP Server** - Automatic IP assignment

## 📐 What I Did (Step by Step)

### 1. Network Topology Design
- Created a network diagram with core switch, distribution layer, and access layer
- Placed wireless access points strategically for coverage
- Connected WLC to the core network for centralized control

### 2. Wireless Configuration
- Configured multiple SSIDs:
  - `Corporate-Secure` (WPA2-Enterprise)
  - `Guest-WiFi` (WPA2-Personal, isolated VLAN)
- Set up VLAN segmentation for security isolation
- Configured wireless security policies

### 3. IP Addressing & DHCP
- Designed subnet: `192.168.10.0/24` for wireless clients
- Configured DHCP scope on the router
- Set up DHCP relay on the WLC

### 4. Security Implementation
- Enabled WPA2-Enterprise with RADIUS authentication
- Configured guest network isolation (no access to internal resources)
- Implemented MAC filtering for authorized devices

## 📸 Screenshots
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/44c43fa0-afbd-4b22-a661-614519134861" />


## ✅ What I Learned
- How wireless networks are architected in enterprise environments
- The importance of VLAN segmentation for wireless security
- How WLCs centralize wireless management
- Real-world wireless security best practices (WPA2-Enterprise vs WPA2-Personal)
- DHCP configuration in multi-VLAN environments

## 📁 Files in This Folder
- `wireless-network-design.pkt` - Cisco Packet Tracer project file
- `README.md` - This documentation
- `screenshots/` - Folder with project screenshots
