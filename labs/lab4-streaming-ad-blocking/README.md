# Raspberry Pi Lab 4 – Pi-hole Network-Wide Ad Blocking
This lab demonstrates how to install, configure, and verify Pi-hole on a Raspberry Pi 4 to enable network-wide ad blocking. The process includes installation, DNS configuration, blocklist updates, and dashboard verification.

---

## 📌 Lab Overview
**Objective:**  
Deploy Pi-hole on Raspberry Pi to filter ads, trackers, and malicious domains across the network using DNS-level blocking.

**Skills Learned**
- Raspberry Pi OS administration  
- Network DNS management  
- Pi-hole installation & configuration  
- Managing blocklists  
- Router-level DNS configuration  
- Verifying network-wide DNS filtering  

**Equipment Used**
- Raspberry Pi 4 (8GB)  
- Raspberry Pi OS (Debian Bookworm)  
- Netgear R8000P Router  
- Terminal (SSH)  
- Chrome Browser (Pi-hole Web UI)

---

## 🖥️ Step-by-Step Screenshots

### 1. Pi-hole Installer – Welcome Screen  
![RPi4-01](RPi4-01_PiHoleInstaller_Welcome.png)

### 2. Interface Selection  
![RPi4-02](RPi4-02 — Interface Selection.png)

### 3. Static IP Confirmation  
![RPi4-02_StaticIP](RPi4-02_StaticIP_Confirmation.png)

### 4. DNS Provider Selection (Cloudflare)  
![RPi4-03](RPi4-03_DNSProvider_Cloudflare.png)

### 5. Privacy Mode Selection  
![RPi4-03b](RPi4-03b_PrivacyMode.png)

### 6. Installation Complete  
![RPi4-05](RPi4-05_Installation_Complete.png)

### 7. Pi-hole Dashboard (Initial View)  
![RPi4-06](RPi4-06_Dashboard_Main.png)

### 8. Adlists Added  
![RPi4-07](RPi4-07_Adlists_Added.png)

### 9. Updating Blocklists (Gravity Update)  
![RPi4-08](RPi4-08_Update_Gravity.png)

### 10. Final Dashboard Verification (DNS Working)  
![RPi4-09](RPi4-09_Final_Dashboard.png)

---

## 📡 Router DNS Setup (Netgear R8000P)
To ensure all devices use Pi-hole automatically, DNS was set on the router:

**Primary DNS:** `192.168.1.5`  
**Secondary DNS:** `1.1.1.1`

**Result:**  
All clients on the network now route DNS through Pi-hole → ads and trackers are filtered automatically.

---

## 🔍 Verification
Traffic began flowing into Pi-hole immediately after DNS was updated in the router:

- Blocklists loaded: **301,223 domains**
- DNS queries flowing: ✔️  
- Ads blocked on all devices: ✔️  
- Pi-hole responding at: **http://192.168.1.5/admin**

---

## ✅ Lab Complete
Pi-hole is successfully installed, configured, and running as the primary DNS server for the home network. Ads, trackers, and malicious domains are now being filtered at the DNS level.