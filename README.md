# 🛡️ Enterprise Network Security: Layer 2 Hardening & WLAN Deployment

![Cisco](https://img.shields.io/badge/Cisco-CCNA-blue?logo=cisco)
![Network Security](https://img.shields.io/badge/Security-Layer_2_Defenses-green)
![License](https://img.shields.io/badge/License-MIT-green)

## 📚 Table of Contents
1. [📋 Project Overview](#1-project-overview)
2. [🔐 Key Security Implementations](#2-key-security-implementations)
3. [📝 Technical Documentation](#3-technical-documentation)
4. [🌐 Network Topologies](#4-network-topologies)
5. [🛡️ Attack Mitigations](#5-attack-mitigations)
6. [⚙️ Configuration Examples](#6-configuration-examples)
7. [🔗 References](#7-references)

---

<a id="1-project-overview"></a>
## 📋 1. Project Overview

**👤 Client**: Microtech Sdn. Bhd (Kuala Lumpur HQ & Brunei Branch)  
**🎯 Objective**: Secure enterprise network against Layer 2 attacks while implementing resilient WLAN architecture.

### 🧩 Core Components
- 📡 WLAN Controller with 4 Lightweight APs  
- 🗂️ VLAN segmentation (HR / Design / Delivery / Management)  
- 🛡️ Layer 2 hardening against:
  - 🧨 MAC Flooding  
  - ⚠️ Rogue DHCP  
  - 🧷 STP Manipulation  

---

<a id="2-key-security-implementations"></a>
## 🔐 2. Key Security Implementations

### 🧱 Layer 2 Defenses

| 🚨 Attack Type       | 🛡️ Mitigation Strategy               | 🛠️ Implementation Example             |
|----------------------|--------------------------------------|----------------------------------------|
| MAC Flooding         | Port Security + AAA Authentication   | `switchport port-security maximum 2`   |
| Rogue DHCP Server    | DHCP Snooping + Disabled Ports       | `ip dhcp snooping vlan 10,20,30`       |
| STP Manipulation     | BPDU Guard + Root Guard              | `spanning-tree bpduguard enable`       |

### 📶 Wireless Security

```cisco
interface WLC-Management
 ip address 192.168.100.254 255.255.255.0
!
wlan SECURE_WLAN 1 WPA2-ENTERPRISE
 radius-server host 192.168.50.10
```

---

<a id="3-technical-documentation"></a>
## 📝 3. Technical Documentation

📌 Full project details cover:

- 🗺️ Network topology diagrams (HQ and Brunei branch)  
- ⚙️ WLC implementation methodology  
- 🧪 Layer 2 attack simulations:
  - MAC Flooding demonstration  
  - Rogue DHCP server setup  
  - STP manipulation techniques  
- 🧾 Defense configuration templates  

---

<a id="4-network-topologies"></a>
## 🌐 4. Network Topologies

### 🏢 HQ Logical Topology

```
[Core Switch]---[Firewall]---[Internet]
   |      |      |
  HR    Design  Delivery
VLANs: 10     20        30
```

### 🏝️ Brunei Wireless Topology

```
[AP1]----[WLC]----[Core Switch]
[AP2]     |        [Admin PC]
[AP3]              (192.168.100.2)
[AP4]
```

---

<a id="5-attack-mitigations"></a>
## 🛡️ 5. Attack Mitigations

### 🧨 MAC Flooding Defense

```cisco
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
end
```

### 🚫 Rogue DHCP Prevention

```cisco
ip dhcp snooping
ip dhcp snooping vlan 10,20,30
interface GigabitEthernet0/1
 ip dhcp snooping trust
```

### 🔐 STP Hardening

```cisco
spanning-tree portfast bpduguard default
spanning-tree vlan 10,20,30 root primary
```

---

<a id="6-configuration-examples"></a>
## ⚙️ 6. Configuration Examples

### 🗂️ VLAN Segmentation

```cisco
vlan 10
 name HR
vlan 20 
 name Design
vlan 30
 name Delivery
!
interface GigabitEthernet0/1
 switchport trunk allowed vlan 10,20,30
 switchport mode trunk
```

---

<a id="7-references"></a>
## 🔗 7. References

- 📘 Cisco Port Security Guide  
- 📗 STP Security Best Practices  
- 📙 DHCP Snooping Configuration  

---

## 📄 License  
MIT © [Your Name]
