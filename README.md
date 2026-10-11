# 🌐 Two-Building Enterprise Network Simulation

> Cisco Packet Tracer project: 4 routers, multi-VLAN, RIPv2 dynamic routing, DHCP, VoIP, wireless, and ACL across two buildings.

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco-Packet%20Tracer-1BA0D7?logo=cisco&logoColor=white)
![Routing](https://img.shields.io/badge/Routing-RIPv2-blue)
![VLAN](https://img.shields.io/badge/VLAN-802.1Q-green)
![VoIP](https://img.shields.io/badge/VoIP-Telephony%20Service-orange)

---

## 📖 Project Overview

This project simulates an enterprise network spanning **two buildings (Gedung A and Gedung B)**. Each building has a *main* (Utama) zone and a *branch* (Cabang) zone, each served by its own router and switch. The four routers are connected in a ring through serial WAN links and exchange routes dynamically with **RIPv2**.

The design covers:

- Network segmentation with multiple **VLANs**
- **Inter-VLAN routing** using router-on-a-stick (802.1Q sub-interfaces)
- Automatic addressing with **DHCP** pools per VLAN
- **VoIP** with Cisco IP Phones using `telephony-service`
- **Wireless LAN** with access points in both buildings
- A centralized **server** (DNS) in Gedung B
- Traffic filtering with **ACL**

---

## 🗺️ Network Topology

![Network Topology](images/topologi.png)

### Zones

| Building | Zone | Router | Switch |
|----------|------|--------|--------|
| Gedung A | Utama (Main) | Router Gedung A Utama | Switch Gedung A Utama |
| Gedung A | Cabang (Branch) | Router A Utama Cabang | Switch Gedung A Cabang |
| Gedung B | Utama (Main) | Router Gedung B Utama | Switch Gedung B Utama |
| Gedung B | Cabang (Branch) | Router Gedung B Cabang | Switch Gedung B Cabang |

---

## 📋 VLAN & Subnet Table

| Building | Zone | VLAN | Subnet | Devices |
|----------|------|------|--------|---------|
| A | Utama | 30 | 192.44.30.0 | PC0, PC1, PC2 |
| A | Cabang | 20 | 198.32.30.0 | Smartphone0, Laptop0 (via Access Point Gedung A) |
| A | Cabang | 21 | 197.73.30.0 | PC3, PC4, PC5 |
| B | Utama | 10 | 192.29.30.0 | Printer0 |
| B | Utama | 11 | 100.100.30.0 | Server0 (DNS) |
| B | Cabang | 50 | 192.123.30.0 | Tablet PC0, Smartphone1 (via Access Point Gedung B) |
| B | Cabang | 100 | 200.20.30.0 | IP Phone0, IP Phone1, IP Phone2 |

<!-- TODO: add the subnet mask for each VLAN (for example /24) -->

> **Note:** IP ranges in this lab are simulation addresses and do not follow RFC 1918 private ranges.

---

## 🔗 WAN Links (Serial)

| Link | Subnet |
|------|--------|
| Router Gedung A Utama ↔ Router Gedung B Utama | 188.55.30.0 |
| Router Gedung A Utama ↔ Router A Utama Cabang | 192.88.30.0 |
| Router Gedung B Utama ↔ Router Gedung B Cabang | 192.66.30.0 |
| Router A Utama Cabang ↔ Router Gedung B Cabang | 192.69.30.0 |

The four routers form a **ring**, so traffic still has an alternate path if one link goes down.

---

## ⚙️ Technologies Used

| Technology | Purpose |
|------------|---------|
| VLAN & 802.1Q trunking | Separate traffic by function (data, wireless, server, voice) |
| Router-on-a-stick | Inter-VLAN routing with sub-interfaces |
| RIPv2 | Dynamic routing between the four routers |
| DHCP | Automatic IP assignment per VLAN |
| Telephony Service (CME) | IP Phone registration and calling between extensions |
| Access Points | Wireless access for smartphones, laptops, and tablets |
| ACL | Restrict traffic between segments |
| DNS Server | Name resolution inside the network |

---

## 🛡️ Access Control List (ACL)

<!-- TODO: describe what your ACL does, for example which VLAN is blocked from reaching which network or server -->

| ACL | Applied On | Purpose |
|-----|------------|---------|
| ... | ... | ... |

---

## 🔧 Device Configurations

Full configurations for every device are stored in the [`configs/`](configs/) folder.

**Routers**
- [Router Gedung A Utama](configs/Router-A-Utama.txt)
- [Router A Utama Cabang](configs/Router-A-Cabang.txt)
- [Router Gedung B Utama](configs/Router-B-Utama.txt)
- [Router Gedung B Cabang](configs/Router-B-Cabang.txt)

**Switches**
- [Switch Gedung A Utama](configs/Switch-A-Utama.txt)
- [Switch Gedung A Cabang](configs/Switch-A-Cabang.txt)
- [Switch Gedung B Utama](configs/Switch-B-Utama.txt)
- [Switch Gedung B Cabang](configs/Switch-B-Cabang.txt)

<!-- Rename the links above so they match your actual file names in configs/ -->

---

## ✅ Verification & Testing

| Test | Command / Method | Expected Result |
|------|------------------|-----------------|
| VLAN & port assignment | `show vlan brief` on every switch | Ports appear in the correct VLAN |
| Trunk links | `show interfaces trunk` | Trunk ports carry the needed VLANs |
| Routing table | `show ip route` on every router | Routes to all subnets learned via RIP (`R`) |
| RIP neighbors | `show ip protocols` | RIPv2 active, all networks advertised |
| DHCP | Set a PC to DHCP | PC receives IP, gateway, and DNS |
| Connectivity | `ping` between buildings | Replies from other building and from the server |
| VoIP | Call from one IP Phone to another | Call connects between extensions |
| DNS | Open the server name from a PC | Name resolves to the server IP |

---

## 📁 Repository Structure

```
.
├── README.md
├── images/
│   └── topologi.png
├── configs/
│   ├── Router-*.txt
│   └── Switch-*.txt
└── packet-tracer/
    └── network-simulation.pkt
```

## 🚀 How to Run

1. Install [Cisco Packet Tracer](https://www.netacad.com/cisco-packet-tracer).
2. Open the `.pkt` file inside the `packet-tracer/` folder.
3. Wait until all links turn green, then run the tests above.

---

## 👤 Author

**Revan Anugrah Wibowo**
Network Engineering student (TJKT), SMKN 3 Kota Tangerang

[LinkedIn](https://www.linkedin.com/in/revan-anugrah-wibowo/)
