# Enterprise Network Hardening: Layer 2 Security & High Availability  
*Cisco-based project implementing defensive controls against network attacks and ensuring redundancy.*

## 🔐 Key Features  
- **Layer 2 Security**  
  - Port Security, DHCP Snooping, BPDU Guard against MAC flooding/rogue DHCP/STP attacks  
  - VLAN segmentation (HR/Design/Delivery/Management)  
  - Blackhole VLAN for unused ports  

- **High Availability**  
  - HSRP for gateway redundancy (Active/Standby routers)  
  - OSPF dynamic routing with passive interfaces  

- **Secure Management**  
  - SSHv2 with RSA encryption (1024-bit keys)  
  - AAA local authentication for device access  

- **Automated Services**  
  - DHCP scopes with reserved IP ranges  
  - EtherChannel (LACP) for trunk redundancy  

## 🛠️ Configuration Files  
| File | Purpose |  
|------|---------|  
| [HQ_Switch.txt](/configs/HQ_Switch.txt) | VLANs, trunking, port security |  
| [Router_OSPF_HSRP.txt](/configs/Router_OSPF_HSRP.txt) | Routing and gateway redundancy |  
| [WLC_Setup.txt](/configs/WLC_Setup.txt) | Wireless LAN Controller (WPA2, RADIUS) |  

## 🔧 How to Replicate  
1. **Layer 2 Hardening**  
   ```bash
   # Enable port security on access ports
   interface FastEthernet0/1
   switchport port-security
   switchport port-security maximum 1
   switchport port-security mac-address sticky
