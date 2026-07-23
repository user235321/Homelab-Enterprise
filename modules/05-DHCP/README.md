# Dynamic Host Configuration Protocol (DHCP)

## Overview

The Dynamic Host Configuration Protocol (DHCP) service was deployed to automate IP address assignment within the laboratory. By centralizing network configuration, DHCP simplifies the deployment of new devices and ensures consistent network settings across the environment.

The DHCP role is hosted on the Domain Controller, providing automatic IP configuration for all domain-joined systems.

---

# Why DHCP

DHCP eliminates the need to manually configure network settings on each device.

By automatically assigning IP addresses and network parameters, DHCP reduces configuration errors and improves the scalability of the infrastructure.

Within this laboratory, DHCP provides consistent network configuration while supporting the Active Directory environment.

---

# DHCP Architecture

```
                    +----------------------+
                    | Windows Server       |
                    | DHCP Server          |
                    +----------+-----------+
                               |
               Assigns network configuration
                               |
         +---------------------+----------------------+
         |                                            |
         v                                            v
+----------------------+                 +----------------------+
| Windows 11 Client    |                 | Ubuntu Server        |
+----------------------+                 +----------------------+
```

---

# DHCP Scope

A single DHCP scope was configured for the internal network.

| Property | Value |
|----------|-------|
| Scope Name | Internal LAN |
| Network | 192.168.1.0/24 |
| Default Gateway | 192.168.1.1 |
| DNS Server | Domain Controller |
| Domain Name | home.lab |

The scope provides IP addresses to all devices connected to the internal network.

---

# Scope Options

The following DHCP options were configured:

| Option | Purpose |
|---------|---------|
| Router (Default Gateway) | pfSense LAN Interface |
| DNS Server | Windows Server Domain Controller |
| DNS Domain | home.lab |

These options ensure that every client receives the correct network configuration automatically.

---

# Lease Configuration

DHCP leases are assigned automatically when clients join the network.

The default lease duration provided by Windows Server is sufficient for the current laboratory environment.

---

# DHCP Reservations

No DHCP reservations have been configured in the current version of the laboratory.

At this stage, dynamic address allocation fully satisfies the requirements of the environment.

Future versions may introduce reservations for infrastructure servers or other devices requiring fixed IP addresses.

---

# Address Assignment

Each client automatically receives:

- IPv4 Address
- Subnet Mask
- Default Gateway
- DNS Server
- DNS Suffix

This eliminates manual network configuration and ensures consistent settings across all systems.

---

# Validation

The DHCP deployment was validated by confirming:

- Successful IP address assignment
- Successful gateway configuration
- Successful DNS configuration
- Successful communication with the Domain Controller
- Successful Internet connectivity through pfSense

Validation commands:

```powershell
ipconfig /all

ipconfig /release

ipconfig /renew
```

---

# Lessons Learned

This module provided practical experience with:

- Windows DHCP Server
- DHCP Scopes
- Scope Options
- Automatic Address Assignment
- Enterprise Network Configuration
- DHCP Troubleshooting

---

# References

- Microsoft Learn
- Windows Server DHCP Documentation