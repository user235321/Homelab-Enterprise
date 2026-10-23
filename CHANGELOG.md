# Changelog

All notable changes to this project will be documented in this file.

This project follows a continuous improvement approach as new infrastructure components, security controls and documentation are added.

---

## [1.1.0] - 2026-10-23

### Added

- Ubuntu storage server: software RAID 5 (mdadm) + LVM + NFS, with a disk-failure and rebuild test
- Wazuh module: centralised logging, detection, active response, Sysmon and SCA
- Attack Scenarios module: Kali intrusion testing and defence validation

### Changed

- DHCP documented on pfSense (previously stated as the Domain Controller)
- Group Policy updated to the real 9 GPOs, with LDAP signing enforced and department drive mapping
- Active Directory updated with the real OU structure and Windows Server 2022
- Overview updated to six virtual machines

---

## [1.0.0] - Initial Release

### Added

- VMware Workstation infrastructure
- pfSense firewall
- Windows Server Domain Controller
- Windows 11 Enterprise client
- Ubuntu Server virtual machine
- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- Windows hardening
- Technical documentation
- Roadmap
- Troubleshooting guide

### Security

- SMB Signing enabled
- SMBv1 disabled
- NTLM hardening
- LDAP Signing enabled
- PowerShell Module Logging
- PowerShell Script Block Logging
- Windows auditing
- AutoRun disabled

### Documentation

- Infrastructure overview
- VMware documentation
- pfSense documentation
- Active Directory documentation
- DNS documentation
- DHCP documentation
- Group Policy documentation
- Windows Hardening documentation
- Ubuntu Server documentation
- Troubleshooting guide
- Project roadmap

---

## Upcoming

Planned future improvements include:

- Wazuh
- Sysmon
- Windows Event Forwarding (WEF)
- Docker
- SSH Hardening
- Active Directory Certificate Services (AD CS)
- Microsoft LAPS
- Additional enterprise services