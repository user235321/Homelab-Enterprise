# Ubuntu Server

## Overview

An Ubuntu Server virtual machine was deployed to introduce a Linux-based system into the laboratory.

Although the current implementation is intentionally simple, the server provides a foundation for future services and allows the environment to simulate a mixed Windows/Linux enterprise infrastructure.

The Ubuntu server will be expanded in future versions of the laboratory as additional services are introduced.

---

# Installation

Ubuntu Server was installed as a dedicated virtual machine within VMware Workstation Pro.

The installation was performed using the default server configuration with only the components required for this laboratory.

---

# Network Configuration

The Ubuntu Server is connected to the internal laboratory network.

Network configuration allows communication with:

- Domain Controller
- Windows Client
- pfSense

The server has Internet access through the pfSense gateway while remaining isolated from the host network.

---

# Hostname Configuration

A hostname was configured to uniquely identify the server within the laboratory.

Using meaningful hostnames simplifies administration and troubleshooting as the environment grows.

---

# Installed Packages

The current installation contains only the packages required for a minimal server deployment.

Additional packages and services will be installed as new modules are added to the laboratory.

---

# System Updates

The operating system was fully updated after installation to ensure the latest security patches and package versions were applied.

Typical update commands include:

```bash
sudo apt update

sudo apt upgrade
```

---

# Purpose within the Lab

At the current stage of the project, the Ubuntu Server is used to:

- Introduce Linux administration into the environment
- Validate communication between Linux and Windows systems
- Provide a platform for future infrastructure services
- Support future cybersecurity exercises

Future implementations may include:

- SSH
- Docker
- Wazuh Agent
- Syslog
- File Services
- Monitoring Tools

---

# Validation

The Ubuntu deployment was validated by confirming:

- Successful installation
- Successful boot
- Network connectivity
- Internet connectivity
- Communication with the Windows environment
- Successful package updates

Validation commands:

```bash
hostname

ip addr

ping 192.168.1.1

ping google.com

apt list --upgradable
```

> *(Screenshot of Ubuntu terminal will be added here.)*

---

# Lessons Learned

This module provided practical experience with:

- Ubuntu Server installation
- Linux networking
- Package management
- Linux command line
- VMware virtual machines
- Enterprise infrastructure integration

---

# References

- Ubuntu Server Documentation
- Ubuntu Package Management Documentation