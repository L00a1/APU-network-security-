# Enterprise Network Security: Layer 2 Hardening & WLAN Deployment

![Cisco](https://img.shields.io/badge/Cisco-CCNA-blue?logo=cisco)
![Network Security](https://img.shields.io/badge/Security-Layer_2_Defenses-green)

A comprehensive implementation of Layer 2 security controls and WLAN architecture for Microtech Sdn. Bhd, addressing critical network vulnerabilities.

## 📖 Table of Contents
- [Project Overview](#-project-overview)
- [Key Security Implementations](#-key-security-implementations)
- [Technical Documentation](#-technical-documentation)
- [Network Topologies](#-network-topologies)
- [Attack Mitigations](#-attack-mitigations)
- [Getting Started](#-getting-started)
- [References](#-references)

## 🌐 Project Overview
**Client**: Microtech Sdn. Bhd (Kuala Lumpur HQ & Brunei Branch)  
**Objective**: Secure enterprise network against Layer 2 attacks while implementing a resilient WLAN architecture.

### Core Components:
- **WLAN Controller (WLC)** deployment with 4 Lightweight APs
- **VLAN segmentation** for HR/Design/Delivery departments
- **Layer 2 hardening** against:
  - MAC Flooding
  - Rogue DHCP
  - STP Manipulation

## 🔒 Key Security Implementations

### Layer 2 Defenses
| Attack Type          | Mitigation Strategy                          | Tools Used              |
|----------------------|---------------------------------------------|-------------------------|
| MAC Flooding         | Port Security + AAA Authentication          | Cisco IOS Port Security |
| Rogue DHCP Server    | DHCP Snooping + Disabled Unused Ports       | DHCP Guard              |
| STP Manipulation     | BPDU Guard + Root Guard                     | STP Hardening           |

### WLAN Architecture
cisco
WLC Configuration Snippet
interface WLC-Management
 ip address 192.168.100.254 255.255.255.0
wlan SECURE_WLAN 1 WPA2-ENTERPRISE
  radius-server host 192.168.50.10


###📄 Technical Documentation

Full project report available in:

Report.pdf (14-page detailed analysis)

Key sections:

Network topology diagrams

WLC implementation guide

Layer 2 attack simulations

Defense configuration snippets

##🌉 Network Topologies

Logical Topology
HQ Network
Figure 1: Kuala Lumpur HQ Architecture

Wireless Topology
plaintext
Copy
Brunei Branch WLAN:
AP1 ---- WLC (192.168.100.254) ---- Core Switch
AP2       |
AP3    Admin PC (192.168.100.2)
AP4
##🛡️ Attack Mitigations
MAC Flooding Defense
cisco
Copy
! Port Security Configuration
interface FastEthernet0/1
 switchport port-security
 switchport port-security maximum 2
 switchport port-security violation restrict
 switchport port-security mac-address sticky
STP Protection
cisco
Copy
! BPDU Guard Implementation
spanning-tree portfast bpduguard default
🚀 Getting Started
Lab Recreation
Base Requirements:

Cisco switches (2960/X)

Wireless LAN Controller

4 Lightweight APs

Configuration Steps:

bash
Copy
# Apply port security template
configure terminal
interface range fa0/1-24
switchport port-security
end
