# Domain Name System (DNS)

## Overview

The Domain Name System (DNS) was deployed as a core infrastructure service within the Active Directory environment. DNS provides reliable name resolution for all systems connected to the domain and is essential for Active Directory functionality.

The DNS service allows domain-joined devices to locate network resources, authenticate with the Domain Controller and communicate using hostnames instead of IP addresses.

---

# Why DNS

DNS is a fundamental component of every Active Directory environment.

Without DNS, clients would not be able to locate domain services, authenticate users or discover domain controllers.

For this reason, the DNS role was installed directly on the Domain Controller.

---

# DNS Architecture

The laboratory uses a centralized DNS architecture.

| Component | Description |
|-----------|-------------|
| DNS Server | Windows Server Domain Controller |
| DNS Zone Type | Active Directory Integrated |
| Primary Zone | home.lab |

This configuration allows all domain services to rely on a single authoritative DNS server.

---

# Forward Lookup Zone

A Forward Lookup Zone was created for the **home.lab** domain.

This zone stores hostname-to-IP address mappings, allowing systems to resolve hostnames into IPv4 addresses.

Examples include:

- Domain Controller
- Windows Client
- Ubuntu Server

---

# Reverse Lookup Zone

A Reverse Lookup Zone was configured to support reverse DNS lookups.

This allows IP addresses to be resolved back into hostnames, improving troubleshooting and network diagnostics.

---

# Dynamic DNS

Dynamic DNS updates are enabled through Active Directory.

When domain-joined devices receive an IP address, their DNS records are automatically created and updated without manual intervention.

---

# Name Resolution Process

Name resolution within the laboratory follows the standard Active Directory process.

1. Client requests name resolution.
2. Query is sent to the Domain Controller.
3. DNS searches the appropriate zone.
4. The corresponding IP address is returned to the client.

---

# DNS Records

The following DNS record types are used within the laboratory:

| Record Type | Purpose |
|-------------|---------|
| A | Maps hostnames to IPv4 addresses |
| PTR | Resolves IP addresses back to hostnames |
| SRV | Allows clients to locate Active Directory services |

These records are sufficient to support authentication, name resolution and Active Directory service discovery within the current environment.

---

# Validation

The DNS deployment was validated by confirming:

- Successful hostname resolution
- Successful reverse lookup
- Successful domain authentication
- Successful Active Directory service discovery
- Successful communication between all virtual machines

Validation commands:

```powershell
nslookup dc01.home.lab

ping dc01.home.lab

ipconfig /all
```


---

# Lessons Learned

This module provided practical experience with:

- Active Directory Integrated DNS
- Forward Lookup Zones
- Reverse Lookup Zones
- Dynamic DNS Updates
- Name Resolution
- DNS Troubleshooting

---

# References

- Microsoft Learn
- Windows Server DNS Documentation