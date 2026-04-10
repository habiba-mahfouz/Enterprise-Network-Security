# 🛡️ Enterprise Network Security & Site-to-Site VPN

A comprehensive Cisco Packet Tracer project demonstrating a secure enterprise network infrastructure connecting two branches (Cairo & Alexandria) through a secure VPN tunnel with advanced Layer 2 and Layer 3 security protocols.

<img width="1207" height="509" alt="ccna" src="https://github.com/user-attachments/assets/0eb75d39-d656-408f-9641-d07ec3e67b8c" />

## 🏗️ Network Architecture
The topology consists of two main branches connected via an ISP Router:
*   **Cairo Branch**: Main local network with DHCP services.
*   **Alexandria Branch**: Server farm with static IP configurations.
*   **VPN Tunnel**: Secure GRE/IPsec tunnel for encrypted communication between branches.
*   **Red Zone (Attacker)**: Simulation of a Rogue DHCP attack to test network resilience.

## 📂 Project Structure
For detailed configuration commands, you can check the pre-configured scripts in the `orders` folder:
*   📄 [ISP Router Config](orders/ISP_Router.txt)
*   📄 [Cairo Router Config](orders/Cairo_Router.txt)
*   📄 [Alexandria Router Config](orders/Alex_Router.txt)
*   📄 [Switch Security Config](orders/Switch_Security.txt)

## 🛠️ Security Implementations & Tasks

This project follows a strict security checklist to ensure a "Defense-in-Depth" posture:

1.  **Device Hardening**: Created encrypted administrative accounts and secure `enable` mode passwords on all routers and switches.
2.  **Secure Management**: Enabled **SSH** on all network nodes to disable insecure Telnet access.
3.  **Port Security**: Implemented Layer 2 security on switches to prevent unauthorized device connections.
4.  **DHCP Snooping**: Mitigated **Rogue DHCP attacks** (Red Zone) by configuring trusted and untrusted ports to ensure clients only receive IPs from the legitimate server.
5.  **IP Management**: 
    *   Configured DHCP pools for Cairo (Range: 192.168.1.1 - 192.168.1.200) with IP exclusions.
    *   Assigned Static IPs for critical Alexandria servers for reliability.
6.  **Site-to-Site Connectivity**: Established a secure **Tunnel** between Cairo and Alexandria.
7.  **Routing Protocol**: Configured **OSPF** to run over the VPN tunnel for dynamic and secure route exchange.
8.  **Connectivity Validation**: Verified that the IT Manager's laptop has full reachability (Ping) to all servers and network switches.

## 🚀 Getting Started
*   **Software**: Cisco Packet Tracer (v8.0 or higher recommended).
*   **Files**: Download the `.pkt` source file from this repository and open it in Packet Tracer.

---
*Developed as a comprehensive Network Security Lab Project.*

