# Troubleshooting

## Overview

This document records the issues encountered during the deployment of the Enterprise Home Lab together with their corresponding solutions.

Rather than simply documenting successful configurations, this section captures real troubleshooting scenarios experienced throughout the project. The objective is to create a reusable knowledge base for future deployments while improving problem-solving skills.

---

# VMware Issues

## Shared Folder Not Working

### Problem

VMware Shared Folders were not accessible from the guest operating system.

### Cause

Shared Folders were not enabled within the virtual machine settings.

### Resolution

- Enabled Shared Folders in VMware settings.
- Rebooted the virtual machine.
- Verified folder accessibility.

---

# Networking Issues

## Virtual Machines Unable to Communicate

### Problem

Virtual machines could not communicate across the internal network.

### Cause

Incorrect VMware virtual network configuration.

### Resolution

- Verified VMnet assignments.
- Confirmed NAT and Host-Only configuration.
- Restarted network adapters.

---

# pfSense Issues

## No Internet Connectivity

### Problem

Client machines could not access the Internet.

### Cause

Incorrect gateway or WAN configuration.

### Resolution

- Verified WAN DHCP configuration.
- Confirmed NAT was functioning.
- Tested Internet connectivity from pfSense.

---

# Active Directory Issues

## Domain Join Failed

### Problem

Windows client could not join the domain.

### Cause

DNS server was incorrectly configured.

### Resolution

- Configured the Domain Controller as the preferred DNS server.
- Verified domain name resolution.
- Successfully joined the domain.

---

# DNS Issues

## Hostname Resolution Failed

### Problem

Clients were unable to resolve hostnames.

### Cause

DNS records had not yet been created or replicated.

### Resolution

- Verified Forward Lookup Zone.
- Used nslookup for troubleshooting.
- Confirmed Active Directory DNS integration.

---

# DHCP Issues

## Client Did Not Receive an IP Address

### Problem

A client failed to obtain an IP address automatically.

### Cause

DHCP scope configuration was incorrect.

### Resolution

- Verified DHCP scope.
- Confirmed DHCP service was running.
- Renewed the DHCP lease.

---

# Group Policy Issues

## Wallpaper Not Applied

### Problem

The desktop wallpaper was not applied after user logon.

### Cause

The shared folder permissions were incorrectly configured.

### Resolution

- Corrected SMB share permissions.
- Executed:

```powershell
gpupdate /force
```

- Logged off and logged back in.

---

# Authentication Issues

## Domain Login Failed

### Problem

Users were unable to authenticate using domain credentials.

### Cause

DNS configuration or network connectivity issues.

### Resolution

- Verified DNS settings.
- Confirmed Domain Controller availability.
- Tested authentication again.

---

# Commands Used

## Windows

```powershell
gpupdate /force

gpresult /r

gpresult /h report.html

ipconfig /all

nslookup

ping

auditpol /get /category:*

Get-WinEvent

Get-SmbServerConfiguration

Get-NetFirewallProfile
```

---

## Linux

```bash
ip addr

hostname

ping

sudo apt update

sudo apt upgrade
```

---

# Lessons Learned

This module highlights the importance of systematic troubleshooting during infrastructure deployment.

Each issue was investigated by identifying the root cause, validating assumptions and applying corrective actions before documenting the final solution.

Maintaining a troubleshooting guide improves repeatability and reduces deployment time for future environments.

---

# References

- Microsoft Learn
- VMware Documentation
- pfSense Documentation
- Ubuntu Documentation