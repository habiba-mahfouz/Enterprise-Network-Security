# 🛡️ Enterprise Network Security & Site-to-Site VPN

A Cisco Packet Tracer project simulating a secure enterprise network connecting two branches — **Cairo** and **Alexandria (HQ)** — through a GRE VPN tunnel running OSPF, with Layer 2/3 hardening and defenses against a simulated Rogue DHCP attack.

<img width="1561" height="621" alt="network" src="https://github.com/user-attachments/assets/890cd05d-73d2-4d7b-ba09-e942f9e10a62" />

## 🏗️ Network Architecture

| Segment | Details |
|---|---|
| **ISP Router** | g0/0 → Cairo (182.0.0.0/24) · g0/1 → Alexandria (162.0.0.0/24) |
| **Cairo Branch** | LAN 192.168.1.0/24 · DHCP pool (excluded 192.168.1.1–200) · DNS 1.1.1.1 · 4 access switches (switch1, 3, 4, 5) |
| **Alexandria (HQ) Branch** | LAN 172.0.0.0/24 · DHCP for laptop/printer · Static IPs for servers · DNS 2.2.2.2 · switch2 |
| **VPN Tunnel** | GRE tunnel, 100.0.0.0/24, between Cairo (182.0.0.2) and Alex (162.0.0.2), routed with OSPF |
| **Red Zone (Attacker)** | Rogue DHCP server (152.0.0.0/24) simulated on switch3 to test DHCP Snooping |

## 📂 Project Structure

Configuration scripts for every device live in the `orders/` folder:

<img width="1920" height="625" alt="ISP" src="https://github.com/user-attachments/assets/10175892-4fcd-4fe1-b82f-383e70fb770d" />

- 📄 [`orders/ISP_Router.txt`](orders/ISP_Router.txt) — ISP router base config, SSH, admin account
- 📄 [`orders/Cairo_Router.txt`](orders/Cairo_Router.txt) — Cairo router: DHCP pool, GRE tunnel, OSPF
- 📄 [`orders/Alex_Router.txt`](orders/Alex_Router.txt) — Alex/HQ router: DHCP pool, GRE tunnel, OSPF
- 📄 [`orders/Switch_Security.txt`](orders/Switch_Security.txt) — Port Security + DHCP Snooping for switch1, switch2, switch3, switch4, switch5

## 📋 Project Requirements

The lab was built to satisfy the following task sheet:

<img width="1600" height="784" alt="requirements" src="https://github.com/user-attachments/assets/b1923a7e-27dc-42e2-802f-a15289dffc2d" />

## 🛠️ Security Implementation Checklist

1. **Device Hardening** — `username admin` with an encrypted secret and an `enable secret` on every router and switch.
2. **Secure Management** — SSH v2 enabled on all nodes; Telnet disabled (`transport input ssh` only).
3. **Port Security** — sticky MAC, max 1 per access port, on every port facing an end device (PCs, IT Manager, servers, printer, laptop).
4. **DHCP Snooping** — enabled on all switches; only the uplink chain back to the legitimate Cairo router DHCP server is trusted, so the Rogue DHCP attacker in the Red Zone can never hand out an address.
5. **IP Management**
   - Cairo: DHCP pool 192.168.1.0/24 with 192.168.1.1–192.168.1.200 excluded (covers router, switch mgmt IPs, and IT Manager's static IP).
   - Alexandria: static IPs on the two servers (172.0.0.4, 172.0.0.5); DHCP for the laptop and printer.
6. **Site-to-Site VPN** — GRE tunnel (100.0.0.0/24) between the Cairo and Alexandria routers, sourced/destined on their public ISP-facing interfaces.
7. **Dynamic Routing** — OSPF area 0 runs over the tunnel and both LANs so each branch learns the other's routes automatically.
8. **Connectivity Validation** — the IT Manager's laptop (192.168.1.250) can reach every switch and server on both branches.

## 🖼️ Full Topology Screenshots

Individual close-up screenshots of each part of the network (switches, ISP router, IT Manager, and the attacker zone) are available in the [`topology images/`](topology%20images) folder for a closer look at each segment.

## 🚀 Getting Started

1. Install **Cisco Packet Tracer** (v8.0+ recommended).
2. Clone this repo and open the `.pkt` file.
3. Apply the configs from `orders/` to their matching devices (swap in your actual interface numbers where noted).
4. From the IT Manager laptop, `ping` each switch management IP and each server to confirm end-to-end reachability.

---
*Developed as a comprehensive Network Security Lab Project.*
