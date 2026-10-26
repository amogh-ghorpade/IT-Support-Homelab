# 🖥️ Enterprise IT Support & Active Directory Home Lab

Welcome to my IT Support and Infrastructure Home Lab repository! This repository documents hands-on experience building enterprise-style corporate environments using virtualization, Windows Server administration, Active Directory, and endpoint management.

---

## 🏗️ Lab Architecture & Network Summary
* **Hypervisor:** VMware Workstation Pro[cite: 1]
* **Domain Controller:** Windows Server 2022 (`lab.internal` / `CORP`) — IP: `192.168.10.10`
* **Client Workstation:** Windows 11 Enterprise (`WIN11-PC01`) — IP: `192.168.10.20`
* **Core Services:** Active Directory Domain Services (AD DS), DNS, DHCP, Group Policies

---

## 📚 Documentation Index
* **[01. Active Directory Deployment & Configuration Guide](docs/01-active-directory.md)**
  * Complete step-by-step documentation covering static IP assignment, forest promotion (`lab.internal`), Organizational Unit structuring (`_Company`), Global Security Group creation (`IT-Support`), domain user creation (`jdoe`), and client workstation domain join.

---

## 🎯 Objectives & Skills Demonstrated
* Centralized identity and access management (IAM)
* Enterprise network configuration and SRV record resolution
* Organizational Unit (OU) design for Group Policy management
* Hands-on helpdesk and systems administration troubleshooting
