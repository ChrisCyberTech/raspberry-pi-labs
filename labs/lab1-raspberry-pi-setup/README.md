# Lab 1 — Raspberry Pi Initial Setup & Secure SSH Configuration

This lab prepares the Raspberry Pi for all future projects in the Raspberry Pi Labs series.  
You will flash Raspberry Pi OS, complete first-boot setup, secure the device, enable firewall protection, and configure static networking.

---

## 📌 Lab Objectives
- Flash Raspberry Pi OS using Raspberry Pi Imager  
- Configure localization and first-boot preferences  
- Perform system updates  
- Enable SSH and complete key-based authentication setup  
- Assign a static IP address  
- Enable UFW firewall  
- Apply basic SSH hardening  

---

## 🧰 Tools & Technologies
- **Raspberry Pi 4 (8GB)**
- **Raspberry Pi OS (64-bit)**
- **macOS Terminal**
- **Raspberry Pi Imager**
- **SSH (OpenSSH)**
- **UFW Firewall**
- **Netgear R8000P Router**

---

## 🗂 Folder Structure (Recommended)

lab1-raspberry-pi-setup/
│
├── README.md
└── screenshots/
├── Lab1-01_DeviceSelection.png
├── Lab1-02_OSSelection.png
├── Lab1-03_Localisation.png
├── Lab1-04_WriteVerification.png
├── Lab1-05_WriteComplete.png
├── RPi1-05_Mac_ssh_FirstLogin.png
├── RPi1-06_Terminal_System_Update.png
├── RPi1-07_Static_IP_Config.png
├── RPi1-08_Firewall_Enabled.png
├── RPi1-09_Mac_SSH-Key-Installed.png
└── RPi1-10_SSH-Config_Hardening.png

yaml
Copy code

---

## 🧪 Step-by-Step Summary

### **1️⃣ Flash Raspberry Pi OS**
Using Raspberry Pi Imager, select:
- **Device:** Raspberry Pi 4
- **OS:** Raspberry Pi OS (64-bit)
- Configure:
  - Hostname  
  - Username/password  
  - Wi-Fi  
  - Locale  
  - SSH enabled  

📸 **Screenshot:**  
`Lab1-01_DeviceSelection.png`

---

### **2️⃣ OS Selection**
Choose Raspberry Pi OS 64-bit.

📸 **Screenshot:**  
`Lab1-02_OSSelection.png`

---

### **3️⃣ Localization Configuration**
Set:
- Timezone  
- Keyboard layout  
- Language  

📸 **Screenshot:**  
`Lab1-03_Localisation.png`

---

### **4️⃣ OS Writing & Verification**
Imager writes the OS and verifies your SD card.

📸 **Screenshots:**
- `Lab1-04_WriteVerification.png`
- `Lab1-05_WriteComplete.png`

---

### **5️⃣ First Login via SSH (Mac)**
Connect to Pi using SSH:  
ssh pi@<PI-IP>

yaml
Copy code

📸 **Screenshot:**  
`RPi1-05_Mac_ssh_FirstLogin.png`

---

### **6️⃣ System Update**
After logging in:
sudo apt update && sudo apt upgrade -y

yaml
Copy code

📸 **Screenshot:**  
`RPi1-06_Terminal_System_Update.png`

---

### **7️⃣ Configure Static IP**
Edit:
sudo nano /etc/dhcpcd.conf

makefile
Copy code
Add:
interface wlan0
static ip_address=192.168.1.X/24
static routers=192.168.1.1
static domain_name_servers=1.1.1.1

yaml
Copy code

📸 **Screenshot:**  
`RPi1-07_Static_IP_Config.png`

---

### **8️⃣ Enable Firewall (UFW)**
Commands:
sudo apt install ufw -y
sudo ufw allow ssh
sudo ufw enable

yaml
Copy code

📸 **Screenshot:**  
`RPi1-08_Firewall_Enabled.png`

---

### **9️⃣ Install SSH Key (Mac → Pi)**
Generate key (if needed):
ssh-keygen -t ed25519

powershell
Copy code
Copy key:
ssh-copy-id pi@<PI-IP>

yaml
Copy code

📸 **Screenshot:**  
`RPi1-09_Mac_SSH-Key-Installed.png`

---

### 🔟 SSH Hardening
Disable password login:
sudo nano /etc/ssh/sshd_config

javascript
Copy code

Set:
PasswordAuthentication no
PermitRootLogin no

yaml
Copy code

Restart SSH:
sudo systemctl restart ssh

yaml
Copy code

📸 **Screenshot:**  
`RPi1-10_SSH-Config_Hardening.png`
