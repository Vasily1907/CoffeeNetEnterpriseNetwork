# CoffeeNetEnterpriseNetwork

# CoffeeNet Enterprise Network (CCNA+ Lab)

This project is a simulation of a corporate network built in Cisco Packet Tracer.
It demonstrates real-world campus + branch architecture with redundancy, routing, security, and centralized services.

The goal of this lab is to showcase **practical networking skills**, not just theoretical configuration.

---

## Network Topology

- **Headquarters (HQ)**
  - 2x Layer 3 switches (Distribution)
  - 3x Access switches
  - Edge router with centralized Internet access
  - Internal servers (DHCP, DNS, Web)
- **2 Branch offices**
  - Each branch connected to HQ via WAN serial links
- **Single ISP**
  - Public network with external Web server

---

## Addressing Scheme

| Location | Network |
|-------|--------|
| HQ VLANs | 10.0.0.0/16 |
| Branch 1 | 10.1.20.0/24 |
| Branch 2 | 10.2.20.0/24 |
| WAN Links | 192.168.1.0/30 |
| ISP | 203.0.113.0/30 |
| Public Web | 198.51.100.0/24 |

---

## Implemented Technologies

### Switching & VLANs
- VLAN segmentation (Management, Sales, HR, IT, Servers, Guests)
- Trunking (802.1Q)
- Access layer separation
- No user traffic in VLAN 1

### Inter-VLAN Routing
- SVI-based routing on Layer 3 switches
- Centralized default gateway per VLAN

### High Availability (HSRP)
- HSRP configured on HQ distribution switches
- Virtual gateway (.1) used by all clients
- Active / Standby roles with priority and preemption
- Verified failover without user traffic interruption

### Routing
- OSPF (single area 0)
- All HQ VLANs and Branch networks advertised
- Default route propagated from HQ edge router

### DHCP & DNS (Centralized)
- Central DHCP/DNS server in HQ (Servers VLAN)
- DHCP relay (`ip helper-address`) on SVI interfaces
- Branch clients receive IPs from HQ
- Internal DNS resolution for intranet services

### NAT / Internet Access
- Centralized NAT (PAT) on HQ edge router
- Single public IP toward ISP
- HQ and Branch users access the Internet via HQ
- No NAT on branch routers (routing only)

### Security
- Guest VLAN restricted from internal servers (ACL)
- Separation between user departments
