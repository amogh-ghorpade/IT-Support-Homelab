# Enterprise Active Directory Deployment & Configuration Guide

## 📌 Project Overview
This project documents the design, deployment, and configuration of an enterprise-style Active Directory Domain Services (AD DS) environment hosted locally using VMware Workstation Pro. The architecture consists of a Windows Server 2022 Primary Domain Controller (DC01) and a Windows 11 client workstation (WIN11-PC01).

---

## 🏗️ Environment & Network Architecture

| Parameter | Primary Domain Controller (DC01) | Client Workstation (WIN11-PC01) |
| :--- | :--- | :--- |
| **Hostname** | DC01 | WIN11-PC01 |
| **Operating System** | Windows Server 2022 Standard | Windows 11 Enterprise |
| **Static IP Address** | 192.168.10.10 | 192.168.10.20 |
| **Subnet Mask** | 255.255.255.0 | 255.255.255.0 |
| **Preferred DNS** | 127.0.0.1 (Local) / 192.168.10.10 | 192.168.10.10 (DC01) |
| **DNS Domain Name** | lab.internal | Joined to lab.internal |
| **NetBIOS Domain Name** | CORP | CORP |

---

## 🛠️ Step-by-Step Implementation Steps

### Phase 1: Virtualization & Network Configuration
1. **VM Provisioning:** Built and configured two virtual machines inside VMware Workstation Pro: DC01 and WIN11-PC01.
2. **Static IP Addressing:** Assigned static IPv4 addresses to both machines to ensure reliable enterprise routing and prevent DHCP assignment shifts.
3. **DNS Integration:** Configured WIN11-PC01 to use DC01 (192.168.10.10) as its primary DNS server to enable proper Active Directory SRV record resolution.
4. **Firewall Verification:** Enabled ICMPv4-Inbound rules on DC01 to verify bi-directional network connectivity via ping commands.

### Phase 2: Active Directory Domain Services (AD DS) Promotion
1. **Role Installation:** Installed the Active Directory Domain Services and DNS Server roles on DC01 via Server Manager.
2. **Forest Creation:** Promoted DC01 as a Domain Controller for a new forest (`lab.internal`).
3. **Functional Levels:** Configured both the Forest and Domain functional levels to Windows Server 2016 (the default and optimal baseline for Windows Server 2022 environments).
4. **DSRM & Reboot:** Configured a secure Directory Services Restore Mode (DSRM) password and completed the post-promotion system restart, initializing administrative access via `CORP\Administrator`.

### Phase 3: Directory Structure & Object Provisioning
Using Active Directory Users and Computers (`dsa.msc`):
1. **Organizational Unit (OU) Hierarchy:**
   * Created a top-level administrative OU named `_Company` (prefixed with an underscore for structural organization).
   * Created three granular sub-OUs underneath `_Company`:
     * `Employees` (housing standard user profiles)
     * `Workstations` (housing enterprise computer objects)
     * `Groups` (housing custom security groups)
2. **Security Group Setup:**
   * Created a Global Security Group named `IT-Support` inside the `Groups` OU.
3. **User Account Provisioning:**
   * Created standard domain user John Doe (`jdoe`) inside the `Employees` OU.
   * Enforced strict AD password complexity compliance requirements.
   * Assigned `jdoe` as an active member of the `IT-Support` security group.

### Phase 4: Client Domain Join & Object Management
1. **Domain Join Process:**
   * Configured WIN11-PC01 system properties (`sysdm.cpl`) to join the `lab.internal` domain utilizing `CORP\Administrator` credentials.
   * Verified successful cryptographic handshake resulting in the “Welcome to the lab.internal domain!” confirmation message.
2. **Domain Authentication:** Performed a successful initial user login on the Windows 11 client using the domain user account (`CORP\jdoe`).
3. **Container Relocation:** Located the newly registered WIN11-PC01 computer object in the default `Computers` container and successfully migrated it into the custom `_Company -> Workstations` OU for targeted Group Policy Object (GPO) management.

---

## 🎯 Key Takeaways & Validation
* **Name Resolution:** Confirmed proper client-to-DC name resolution over port 53.
* **Access Control:** Validated centralized authentication across separate physical/virtual nodes.
* **Readiness:** Established a clean, scalable enterprise directory foundation ready for advanced configurations such as GPO security hardening, PowerShell automation scripts, and shared folder permission management.
