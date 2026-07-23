# Enterprise Home Lab

A realistic enterprise home lab designed to develop practical skills in Windows infrastructure, system administration and cybersecurity.

The environment simulates a small enterprise network using VMware, pfSense, Windows Server, Active Directory and Ubuntu Server. Throughout this project, security best practices, Windows hardening techniques and technical documentation are implemented to create a maintainable and scalable enterprise environment.

---

# Project Goals

- Build a realistic enterprise infrastructure
- Deploy and manage Active Directory
- Configure enterprise networking using pfSense
- Implement Windows security hardening
- Apply Group Policy administration
- Document every deployment step
- Create a reusable cybersecurity laboratory

---

# Infrastructure Overview

| Component | Technology |
|-----------|------------|
| Hypervisor | VMware Workstation Pro |
| Firewall | pfSense |
| Domain Controller | Windows Server |
| Client | Windows 11 Enterprise |
| Linux Server | Ubuntu Server |
| Directory Service | Active Directory Domain Services |
| Name Resolution | DNS |
| Address Assignment | DHCP |
| Policy Management | Group Policy |

---

# Infrastructure Diagrams

## Enterprise Architecture

![Enterprise Architecture](diagrams/architecture.png)

---

## Network Topology

![Network Topology](diagrams/network.png)

---

## Active Directory Structure

![Active Directory Structure](diagrams/active-directory.png)

---

## Group Policy Structure

![Group Policy Structure](diagrams/group-policy.png)

---

# Project Structure

```
HOMELAB-ENTERPRISE
│
├── diagrams/
│
├── modules/
│   ├── 00-Overview
│   ├── 01-VMware
│   ├── 02-pfSense
│   ├── 03-Active-Directory
│   ├── 04-DNS
│   ├── 05-DHCP
│   ├── 06-Group-Policy
│   ├── 07-Windows-Hardening
│   ├── 08-Ubuntu
│   └── 09-Troubleshooting
│
├── CHANGELOG.md
├── LICENSE
├── README.md
└── ROADMAP.md
```

---

# Project Modules

| Module | Description |
|---------|-------------|
| 00 - Overview | Project overview and architecture |
| 01 - VMware | Virtualization platform configuration |
| 02 - pfSense | Firewall, networking and routing |
| 03 - Active Directory | Domain Services deployment |
| 04 - DNS | Name resolution infrastructure |
| 05 - DHCP | Dynamic IP address management |
| 06 - Group Policy | Enterprise policy management |
| 07 - Windows Hardening | Security configuration and hardening |
| 08 - Ubuntu | Linux server deployment |
| 09 - Troubleshooting | Deployment issues and solutions |

---

# Technologies

- VMware Workstation Pro
- pfSense
- Windows Server
- Windows 11 Enterprise
- Ubuntu Server
- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- PowerShell

---

# Security Features

- SMB Signing
- SMBv1 Disabled
- NTLM Hardening
- LDAP Signing
- PowerShell Module Logging
- PowerShell Script Block Logging
- Windows Auditing
- AutoRun Disabled

---

# Documentation

Every infrastructure component is fully documented, including:

- Architecture
- Installation
- Configuration
- Validation
- Troubleshooting
- Lessons Learned

---

# Roadmap

Future improvements include:

- Wazuh
- Sysmon
- Windows Event Forwarding (WEF)
- Active Directory Certificate Services (AD CS)
- Microsoft LAPS
- Docker
- Linux Hardening
- Security Monitoring
- Additional Enterprise Services

For the complete roadmap, see:

**[ROADMAP.md](ROADMAP.md)**

---

# Changelog

Project changes are documented in:

**[CHANGELOG.md](CHANGELOG.md)**

---

# License

This project is released under the MIT License.

See:

**[LICENSE](LICENSE)**