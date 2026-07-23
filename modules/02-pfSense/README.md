# pfSense

## Overview

pfSense was deployed as the central firewall and gateway for the laboratory. It provides routing, firewall functionality and network segmentation between the internal enterprise network and the external network, closely simulating the role of a perimeter firewall in a production environment.

---

# Why pfSense

pfSense was selected because it is a widely adopted open-source firewall platform that offers enterprise-grade networking features, including firewall management, routing, DHCP, DNS forwarding and NAT.

For this laboratory, pfSense acts as the central point through which all network traffic is managed.

---

# Network Interfaces

The firewall was configured with two network interfaces.

| Interface | VMware Network | Purpose |
|-----------|----------------|---------|
| WAN | VMnet8 (NAT) | Internet connectivity |
| LAN | VMnet1 (Host-Only) | Internal enterprise network |

---

# WAN Configuration

The WAN interface was configured to obtain its IP address automatically through VMware's NAT network, providing Internet connectivity for the laboratory.

Configuration Summary:

- Address Assignment: DHCP
- Network: VMnet8 (NAT)

---

# LAN Configuration

The LAN interface was configured as the internal enterprise network.

Configuration Summary:

- Static IP Address: 192.168.1.1/24
- VMware Network: VMnet1 (Host-Only)

The LAN network is isolated from the external network and is used for communication between all laboratory systems.

---

# Firewall Rules

The default firewall policy was maintained, allowing controlled communication between internal systems while protecting the laboratory from unsolicited inbound traffic.

---

# DHCP Configuration

The DHCP service was enabled on the LAN interface to automatically assign IP addresses to internal devices.

This ensures that newly connected systems receive consistent network configuration without requiring manual IP assignment.

---

# DNS Configuration

The Domain Controller provides DNS services for the internal network.

pfSense forwards client traffic while the Windows Server is responsible for resolving internal domain names.

---

# Network Address Translation (NAT)

Outbound NAT is enabled to allow devices on the internal network to access external resources through the WAN interface.

This configuration allows all internal systems to share a single external connection.

---

# Routing

pfSense acts as the default gateway for the internal network.

All internal traffic destined for external networks is routed through the firewall.

---

# Validation

The network configuration was validated by confirming:

- Internet connectivity
- Communication between all virtual machines
- DHCP address assignment
- Internal DNS name resolution
- Successful routing through pfSense

---

# Lessons Learned

This module provided practical experience with:

- Firewall deployment
- Enterprise network segmentation
- NAT
- DHCP
- Routing
- Network troubleshooting

---

# References

- pfSense Documentation