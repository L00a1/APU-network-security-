# Enterprise Network Security: Layer 2 Hardening & WLAN Deployment

![Cisco](https://img.shields.io/badge/Cisco-CCNA-blue?logo=cisco)
![Network Security](https://img.shields.io/badge/Security-Layer_2_Defenses-green)
![License](https://img.shields.io/badge/License-MIT-green)

A complete implementation of Layer 2 security controls and WLAN architecture for Microtech Sdn. Bhd, addressing critical network vulnerabilities with Cisco-based solutions.

## Table of Contents
- [Project Overview](#project-overview)
- [Network Architecture](#network-architecture)
- [Layer 2 Attacks](#layer-2-attacks)
- [Security Mitigations](#security-mitigations)
- [Configuration Examples](#configuration-examples)
- [Technical Documentation](#technical-documentation)
- [References](#references)

## Project Overview
**Client**: Microtech Sdn. Bhd (Kuala Lumpur HQ & Brunei Branch)  
**Objective**: Secure enterprise network infrastructure against Layer 2 attacks while implementing resilient WLAN architecture.

### 🔧 Key Components
- WLAN Controller (WLC) with 4 Lightweight APs 📡
- VLAN segmentation (HR/Design/Delivery/Management)
- Layer 2 hardening against:
  - MAC Flooding 🚨
  - Rogue DHCP ⚠️
  - STP Manipulation 🔄

### 🖥️ Technical Stack
- Cisco IOS
- WPA2-Enterprise Authentication 🔐
- RADIUS Server Integration

---

## Network Architecture

### 🏢 HQ Logical Topology
```
[Core Switch]---[Firewall]---[Internet]
    |       |       |
   HR    Design   Delivery
VLANs: 10     20        30
```

### 🌐 Brunei Wireless Topology
```
[AP1]----[WLC]----[Core Switch]
[AP2]     |        [Admin PC]
[AP3]              (192.168.100.2)
[AP4]
```

### 📡 IP Addressing Scheme

| Device      | IP Address         | Subnet Mask       |
|-------------|--------------------|-------------------|
| WLC         | 192.168.100.254    | 255.255.255.0     |
| Admin PC    | 192.168.100.2      | 255.255.255.0     |
| LAPs        | 192.168.100.0/24   | 255.255.255.0     |

---

## Layer 2 Attacks

### 1️⃣ MAC Flooding Attack
**Mechanism**:
- Attacker floods switch with fake MAC addresses
- Overflows CAM table causing fail-open mode
- Switch behaves like hub, enabling packet sniffing

**Diagram**:
```
Attacker → [Fake MACs] → Switch → [Broadcast Traffic] → All Ports
```

---

### 2️⃣ Rogue DHCP Server
**Attack Flow**:
1. Attacker connects rogue DHCP server
2. Responds to DHCP requests faster than legitimate server
3. Assigns malicious gateway or DNS settings

---

### 3️⃣ STP Manipulation
**Technique**:
- Attacker introduces rogue switch with superior BPDU
- Becomes the root bridge
- Redirects traffic for sniffing or modification

---

## Security Mitigations

### 🔐 Port Security Configuration
```cisco
interface FastEthernet0/1
 switchport mode access
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation shutdown
 switchport port-security mac-address sticky
end
```

---

### 🛡️ DHCP Snooping
```cisco
ip dhcp snooping
ip dhcp snooping vlan 10,20,30
interface GigabitEthernet0/1
 ip dhcp snooping trust
```

---

### 🧱 STP Protection
```cisco
spanning-tree portfast bpduguard default
spanning-tree vlan 10,20,30 root primary
```

---

## Configuration Examples

### 🌐 WLC Setup
```cisco
interface WLC-Management
 ip address 192.168.100.254 255.255.255.0
!
wlan SECURE_WLAN 1 WPA2-ENTERPRISE
 radius-server host 192.168.50.10
 authentication open eap
```

---

### 🧩 VLAN Configuration
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

## Technical Documentation

### 🧪 Attack Simulation Results

| Attack Type       | Before Mitigation | After Mitigation         |
|-------------------|-------------------|---------------------------|
| MAC Flooding      | Successful         | Blocked via Port Security |
| Rogue DHCP        | Successful         | Prevented via DHCP Snooping |
| STP Manipulation  | Successful         | Neutralized with BPDU Guard |

---

### ✅ Implementation Checklist
- [x] Deploy port security on all access ports  
- [x] Configure DHCP snooping with trusted ports  
- [x] Enable BPDU guard globally  
- [x] Set up WLC with WPA2-Enterprise  
- [x] Document all security configurations  

---

## References
- 📘 Cisco Port Security Guide  
- 🧷 STP Security Best Practices  
- 📡 DHCP Snooping Configuration Docs  

---

## License
MIT © [Loai-R-Saadia]
