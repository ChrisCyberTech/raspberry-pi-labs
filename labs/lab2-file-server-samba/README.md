# 🐧 Raspberry Pi File Server (PiFS)
**Lab Goal:**  
Configure a Raspberry Pi as a multi-drive SMB file server hosting four external HDDs (Primary1, Secondary, Videos, Temps) with full Mac + Windows 11 compatibility, Samba authentication, and verified read/write functionality.

---

# 📚 Table of Contents
1. [Overview](#overview)  
2. [Hardware Used](#hardware-used)  
3. [Network Topology](#network-topology)  
4. [Step-by-Step Lab Instructions](#step-by-step-lab-instructions)  
5. [Verification Tests](#verification-tests)  
6. [Screenshots](#screenshots)

---

# 📌 Overview
This lab walks through the full deployment of a Raspberry Pi-based file server using **Samba (SMB)** to share multiple external HDDs across macOS and Windows 11 devices.

You will learn how to:

- Update the Pi and install Samba  
- Identify and mount external HDDs  
- Configure proper permissions  
- Edit `smb.conf` to define four shares  
- Create and manage Samba users  
- Connect from macOS Finder and Windows 11 Explorer  
- Perform read/write verification testing on all drives  

---

# 🖥 Hardware Used
- Raspberry Pi 4 (8GB)  
- Four external USB HDDs  
- macOS laptop  
- Windows 11 Laptop  
- 5V/3A Raspberry Pi power supply  
- Pi OS Lite (32-bit)

---

# 🌐 Network Topology

[MacBook] ───┐
│
[Windows PC] ├─── Wi-Fi / LAN ─── [Router] ─── [Raspberry Pi (PiHole + File Server)]
│
[Other Devices] ─┘

yaml
Copy code

Pi IP: **192.168.1.9**

---

# 🛠 Step-by-Step Lab Instructions

---

## **1️⃣ Update & Upgrade the Raspberry Pi**
```bash
sudo apt update && sudo apt upgrade -y
📸 See: PI2-01_Pi_UpdateAndUpgrade.png

2️⃣ Install Samba
bash
Copy code
sudo apt install samba samba-common-bin -y
📸 See: PI2-02_Pi_InstallSamba.png

3️⃣ List All Drives
bash
Copy code
lsblk -f
Identify: Primary1, Secondary, Videos, Temps
📸 See: PI2-03_Pi_ListDrives_lsblk.png

4️⃣ Set Permissions on All Drives
bash
Copy code
sudo chown -R pi:pi /media/pi/Primary1
sudo chmod -R 775 /media/pi/Primary1

sudo chown -R pi:pi /media/pi/Secondary
sudo chmod -R 775 /media/pi/Secondary

sudo chown -R pi:pi /media/pi/Videos
sudo chmod -R 775 /media/pi/Videos

sudo chown -R pi:pi /media/pi/Temps
sudo chmod -R 775 /media/pi/Temps
📸 See: PI2-04_Pi_AllDrives_Permissions.png

5️⃣ Edit Samba Configuration
bash
Copy code
sudo nano /etc/samba/smb.conf
Add the following:

ini
Copy code
[Primary1]
   path = /media/pi/Primary1
   read only = no
   browseable = yes
   valid users = pi
   force user = pi
   create mask = 0775
   directory mask = 0775

[Secondary]
   path = /media/pi/Secondary
   read only = no
   browseable = yes
   valid users = pi
   force user = pi
   create mask = 0775
   directory mask = 0775

[Videos]
   path = /media/pi/Videos
   read only = no
   browseable = yes
   valid users = pi
   force user = pi
   create mask = 0775
   directory mask = 0775

[Temps]
   path = /media/pi/Temps
   read only = no
   browseable = yes
   valid users = pi
   force user = pi
   create mask = 0775
   directory mask = 0775
📸 See: PI2-05_Pi_EditSmbConf_AllShares.png

6️⃣ Restart Samba Services
bash
Copy code
sudo systemctl restart smbd
sudo systemctl restart nmbd
sudo systemctl status smbd --no-pager
📸 See: PI2-06_Pi_SambaService_Restart.png

7️⃣ Create a Samba User
bash
Copy code
sudo smbpasswd -a pi
📸 See: PI2-07_Pi_CreateSambaUser.png

🍎 macOS Connection & Testing
8️⃣ View All Shares in Finder
Finder → Go → Connect to Server →

cpp
Copy code
smb://192.168.1.9
Select volumes.
📸 See: PI2-08_Mac_Finder_AllShares.png

9️⃣ Create Test Folder on Primary1
📸 See: PI2-09_Mac_CreateFolder_Primary1.png

🔟 Create Test Folder on Secondary
📸 See: PI2-10_Mac_CreateFolder_Secondary.png

1️⃣1️⃣ Create Test Folder on Videos
📸 See: PI2-11_Mac_CreateFolder_Videos.png

1️⃣2️⃣ Create Test Folder on Temps
📸 See: PI2-12_Mac_CreateFolder_Temps.png

🪟 Windows 11 Connection & Testing
1️⃣3️⃣ List All Shares in Windows 11
File Explorer →

Copy code
\\192.168.1.9
📸 See: PI2-12_Windows11_AllShares.png

1️⃣4️⃣ Verify All Shares & Folders
Verify the test folders created on macOS appear in Windows.
📸 See: PI2-13_Pi_Verify_AllShares_Folders.png

✍️ Windows → Pi Write Tests
1️⃣5️⃣ Write Test on Primary1
📸 See:

PI2-13_Windows11_WriteTest_Primary1.png

PI2-14_Pi_Verify_WindowsWrite_Primary1.png

1️⃣6️⃣ Write Test on Secondary
📸 See: PI2-15_Windows11_WriteTest_Secondary.png

1️⃣7️⃣ Write Test on Temps
📸 See: PI2-16_Windows11_WriteTest_Temps.png

1️⃣8️⃣ Write Test on Videos
📸 See: PI2-17_Windows11_WriteTest_Videos.png

✅ Verification Summary
Test	macOS	Windows 11
Connect to all shares	✔️	✔️
View all folders	✔️	✔️
Create folders	✔️	✔️
Delete folders	✔️	✔️
Write to all 4 HDDs	✔️	✔️
Permissions correct	✔️	✔️
Samba stable	✔️	✔️

🏁 Lab Completed Successfully
Your Raspberry Pi is now functioning as a fully operational multi-drive SMB file server, accessible by all macOS and Windows devices on your network.

Pi temperature remained stable at ~43°C under load, confirming safe fanless operation.

