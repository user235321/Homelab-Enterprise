# Dynamic Host Configuration Protocol (DHCP)

## Overview

DHCP automates IP address assignment within the laboratory. In this environment the
DHCP service runs on the **pfSense firewall**, on its LAN interface, and is responsible
for handing out IP addresses and network parameters to every device on the internal
network.

Centralising DHCP on the firewall keeps the Windows Domain Controller focused on
identity services (Active Directory and DNS) and avoids running two DHCP servers on the
same segment.

---

# Why DHCP on pfSense

DHCP eliminates the need to configure network settings manually on each device.

Running it on pfSense (rather than on the Domain Controller) was a deliberate choice:

- pfSense already owns the LAN gateway, so it is the natural place to serve addresses.
- It keeps address assignment and routing in one place.
- It avoids having a second DHCP server on the internal network, which would cause
  clients to receive inconsistent configuration.

Only one DHCP server is active on the internal network, which prevents address conflicts.

---

# DHCP Architecture

```
                    +----------------------+
                    | pfSense (LAN)        |
                    | DHCP Server          |
                    | 192.168.1.1          |
                    +----------+-----------+
                               |
               Assigns IP, gateway and DNS
                               |
         +---------------------+----------------------+
         |                                            |
         v                                            v
+----------------------+                 +----------------------+
| Windows 11 Client    |                 | Other LAN devices    |
+----------------------+                 +----------------------+
```

Infrastructure servers that must keep a fixed address (the Domain Controller, the
monitoring server and the storage server) use **static IP addresses** outside the
dynamic range, rather than DHCP.

---

# DHCP Scope

A single DHCP scope was configured on the pfSense LAN interface.

| Property | Value |
|----------|-------|
| Network | 192.168.1.0/24 |
| Default Gateway | 192.168.1.1 (pfSense LAN) |
| DNS Server | Domain Controller (192.168.1.10) |
| Domain Name | home.lab |

The scope provides addresses to client devices on the internal network.

---

# Scope Options

The following DHCP options were configured:

| Option | Value | Purpose |
|---------|-------|---------|
| Router (Default Gateway) | 192.168.1.1 | pfSense LAN interface |
| DNS Server | 192.168.1.10 | Windows Server Domain Controller |
| DNS Domain | home.lab | Internal domain name |

The **DNS server handed out is the Domain Controller, not pfSense**. This is essential in
an Active Directory environment: clients must use the DC for DNS so they can resolve the
domain's SRV records and locate domain services (Kerberos and LDAP). If clients used
pfSense for DNS, domain join and authentication would fail.

---

# Static Addressing

Core infrastructure uses fixed addresses so that services remain reachable at a known IP:

| Host | IP |
|------|-----|
| pfSense (LAN) | 192.168.1.1 |
| Domain Controller | 192.168.1.10 |

Dynamic clients receive the remaining addresses from the DHCP scope.

---

# Validation

The DHCP deployment was validated by confirming:

- Successful IP address assignment on the client
- Correct gateway (192.168.1.1)
- Correct DNS server (the Domain Controller)
- Successful domain authentication
- Internet connectivity through pfSense

Validation commands (Windows client):

```powershell
ipconfig /all

ipconfig /release

ipconfig /renew
```

---

# Lessons Learned

This module provided practical experience with:

- DHCP on pfSense
- DHCP scopes and options
- Serving the correct DNS server for Active Directory
- Avoiding duplicate DHCP servers on a single network
- Planning static vs dynamic addressing

---

# References

- pfSense Documentation
- Microsoft Learn — DNS requirements for Active Directory
