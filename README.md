# Enterprise Home Lab

A realistic enterprise Windows infrastructure laboratory built from scratch to simulate a small production environment.

The primary objective of this project is to gain practical experience with enterprise infrastructure technologies while documenting every implementation step. Rather than focusing on isolated services, this laboratory aims to recreate a realistic Windows domain environment that can be expanded over time with additional security, monitoring and administration solutions.

---

# Project Objectives

The main objectives of this project are:

- Build a realistic enterprise infrastructure
- Deploy and manage Active Directory Domain Services
- Configure DNS and DHCP services
- Implement and manage Group Policy Objects (GPOs)
- Apply Windows security hardening techniques
- Document every implementation step
- Create a reusable platform for future infrastructure and cybersecurity projects

---

# Lab Architecture

> **Architecture diagram will be added here**

---

# Infrastructure Overview

| Component | Technology |
|------------|------------|
| Hypervisor | VMware Workstation Pro |
| Firewall | pfSense |
| Domain Controller | Windows Server |
| Client | Windows 11 Enterprise |
| Linux Server | Ubuntu Server |
| Directory Service | Active Directory |
| Name Resolution | DNS |
| Address Assignment | DHCP |

---

# Technologies Used

## Virtualization

- VMware Workstation Pro

## Networking

- pfSense
- NAT Networking
- Host-Only Networking

## Microsoft Technologies

- Windows Server
- Windows 11 Enterprise
- Active Directory
- Group Policy
- DNS
- DHCP
- PowerShell

## Linux

- Ubuntu Server

---

# Virtual Machines

| Virtual Machine | Purpose |
|-----------------|---------|
| pfSense | Firewall and network gateway |
| Windows Server | Domain Controller |
| Windows 11 Enterprise | Domain client |
| Ubuntu Server | Linux server for future services |

---

# Implemented Features

| Feature | Status |
|----------|--------|
| VMware Infrastructure | ✅ |
| Enterprise Network | ✅ |
| pfSense Firewall | ✅ |
| Windows Server | ✅ |
| Active Directory | ✅ |
| DNS | ✅ |
| DHCP | ✅ |
| Windows Client | ✅ |
| Ubuntu Server | ✅ |
| Group Policy | ✅ |
| Shared Folder Mapping | ✅ |
| Desktop Wallpaper Policy | ✅ |
| Screen Lock Policy | ✅ |
| Command Prompt Restriction | ✅ |
| Password Policy | ✅ |
| Account Lockout Policy | ✅ |
| SMB Signing | ✅ |
| SMBv1 Disabled | ✅ |
| NTLM Hardening | ✅ |
| LDAP Signing | ✅ |
| PowerShell Logging | ✅ |
| Advanced Auditing | ✅ |

---

# Security Baseline

The following security controls have been implemented:

- Password Policy
- Account Lockout Policy
- SMB Signing
- SMBv1 Disabled
- NTLM Hardening
- LDAP Signing
- PowerShell Module Logging
- PowerShell Script Block Logging
- Advanced Windows Auditing
- Command Prompt Restriction

---

# Project Modules

| Module | Description |
|----------|-------------|
| 00 - Overview | General project overview |
| 01 - VMware | Virtual infrastructure |
| 02 - pfSense | Enterprise firewall |
| 03 - Active Directory | Domain infrastructure |
| 04 - DNS | Name resolution |
| 05 - DHCP | IP address management |
| 06 - Group Policy | Enterprise policy management |
| 07 - Windows Hardening | Security configuration |
| 08 - Ubuntu | Linux server |
| 09 - Troubleshooting | Issues encountered and solutions |

---

# Current Project Status

The first version of the laboratory is complete and includes the core services required for a small enterprise environment.

The infrastructure is designed to support future expansion while maintaining clear documentation and reproducible configurations.

---

# Future Improvements

The laboratory will continue to evolve over time.

Planned additions include:

- Sysmon
- Windows Event Forwarding (WEF)
- Wazuh
- Active Directory Certificate Services (AD CS)
- Docker
- Microsoft Defender Configuration
- Additional Windows Hardening
- Linux Hardening
- Monitoring and Logging

---

# Skills Demonstrated

This project demonstrates practical experience with:

- VMware Virtualization
- Enterprise Networking
- Windows Server Administration
- Active Directory
- DNS Administration
- DHCP Administration
- Group Policy Management
- Windows Security Hardening
- PowerShell
- Technical Documentation

---

# References

- Microsoft Learn
- VMware Documentation
- pfSense Documentation
- Ubuntu Documentation

---

# License

This project is licensed under the MIT License.