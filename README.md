# 📘 Labs | Road Map (In Progress)

This roadmap outlines completed, active, and future Raspberry Pi–based IT labs designed to demonstrate hands-on skills across **networking, system administration, cybersecurity, automation, and home-lab engineering**.

These labs progressively build a full ecosystem—including Pi-hole DNS filtering, file services, secure remote access, firewall hardening, and monitoring—mirroring real-world IT workflows.

---

## 📚 Detailed Lab Roadmap

| Lab # | Title | Description |
|-------|--------|-------------|
| **1** | **Raspberry Pi Setup & Secure SSH Configuration** | Complete base installation of Raspberry Pi OS, perform initial OS configuration, enable SSH, secure remote access with key-based authentication, harden SSHD, configure system updates, and assign persistent static IP addressing. |
| **2** | **Raspberry Pi File Server (Samba)** *(Next)* | Build a local network file server using Samba, create shared directories, manage UNIX/Samba users, configure access controls, and test client access from macOS and Windows. Includes directory permissions, service persistence, and troubleshooting connectivity issues. |
| **3** | **Firewall & System Hardening** | Configure host-based firewall rules (UFW), restrict inbound/outbound traffic, block unnecessary services, enable logging, enforce rate limits, and validate rule behavior using real testing tools. Includes SSH hardening and service minimization. |
| **4** | **Pi-hole Deployment + Streaming Ad-Blocking Rules** | Deploy a full Pi-hole DNS filtering system, configure upstream DNS providers, activate privacy modes, add curated blocklists, apply streaming-specific ad-blocking lists, update router DNS settings, and validate network-wide ad filtering. Includes static IP assignment and router MAC/DHCP alignment. |
| **5** | **Secure Remote Access (Advanced SSH)** | Expand remote access capabilities using hardened SSH configurations such as port changes, key-only logins, fail2ban protection, intrusion monitoring, and configuration validation. Includes disaster-recovery access strategies and documented rollback procedures. |
| **6** | **System Monitoring & Health Checks** | Install resource monitoring tools, configure Pi-hole query analytics, set up CPU/memory/disk monitoring, implement log review processes, and create health-check routines. Includes service uptime verification and alerting foundations. |
| **7** | **Pi-hole Local DNS Services & Unbound Integration** *(Planned)* | Integrate Pi-hole with a recursive DNS resolver (Unbound), enable DNSSEC validation, configure local host overrides, implement secure DNS transports (DoH/DoT), and deploy advanced regex filtering. |
| **8** | **Automation Through Cron & Bash Scripting** *(Planned)* | Develop automated maintenance workflows including update scripts, backup jobs, log archival, Pi-hole gravity updates, and system cleanup routines—using cron and shell scripting best practices. |
| **9** | **Raspberry Pi NAS Expansion (Advanced File Services)** *(Planned)* | Expand the file server to support Time Machine backups, multi-user tiered permissions, drive pooling, automounts, and external USB storage configurations. Add snapshot routines and optional RAID through mdadm. |
| **10** | **Home Lab Network Optimization & DHCP Planning** *(Planned)* | Improve network organization through DHCP reservation strategies, VLAN planning, subnet segmentation, performance tuning, router-level logging, and optimization of DNS forwarding paths. Useful for scaling a home-lab environment. |

---

### ✨ Additional Future Modules (Optional Add-Ons)

- **Home VPN Gateway (WireGuard/OpenVPN)**  
  Build a secure VPN endpoint on Raspberry Pi for encrypted remote network access.

- **Intrusion Detection + Log Correlation**  
  Deploy lightweight IDS solutions and centralize system logs for event correlation.

- **Backup/Restore Infrastructure**  
  Automate Pi-hole, Samba, and system config backups using rsync and encrypted archives.

---

### 🏁 Status Indicators (for future addition)

| Symbol | Meaning |
|--------|---------|
| 🟢 | Completed |
| 🟡 | In Progress |
| 🔴 | Planned / Not Started |

---

### 📌 Purpose of This Roadmap

This project serves as a **portfolio showcase** for:

- IT Help Desk & Support Skills  
- System Administration Fundamentals  
- Network Configuration  
- Firewall & Security Hardening  
- Linux Administration  
- Home-Lab Infrastructure Design  
- Documentation & Professional Workflow  

Every lab includes screenshots, step-by-step write-ups, troubleshooting notes, and reproducible procedures.

---

