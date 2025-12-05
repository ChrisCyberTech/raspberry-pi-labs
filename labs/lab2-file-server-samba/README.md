# 🏗️ Raspberry Pi Lab 2 — Samba File Server (Actual Steps Performed)

This lab documents the exact process used to configure a Raspberry Pi as a Samba file server, including macOS and Windows verification. All screenshots included reflect the real workflow executed.

---

# **Step 1 — Update & Upgrade the Raspberry Pi**

```bash
sudo apt update && sudo apt upgrade -y
```

**Screenshot:**  
![PI2-01](./screenshots/PI2-01_Pi_UpdateAndUpgrade.png)

---

# **Step 2 — Install Samba**

```bash
sudo apt install samba -y
```

**Screenshot:**  
![PI2-02](./screenshots/PI2-02_Pi_InstallSamba.png)

---

# **Step 3 — List All Drives (lsblk)**

This confirms all connected external drives and their mount points.

```bash
lsblk -f
```

**Screenshot:**  
![PI2-03](./screenshots/PI2-03_Pi_ListDrives_lsblk.png)

---

# **Step 4 — Apply Permissions to All Drives**

Proper permissions allow Samba users to read/write to shares.

```bash
sudo chown -R pi:pi /media/pi/*
sudo chmod -R 775 /media/pi/*
```

**Screenshot:**  
![PI2-04](./screenshots/PI2-04_Pi_AllDrives_Permissions.png)

---

# **Step 5 — Edit smb.conf and Add All Shares**

Open Samba config:

```bash
sudo nano /etc/samba/smb.conf
```

Add share definitions for your drives:

```
[Primary1]
   path = /media/pi/Primary1
   browseable = yes
   writable = yes

[Secondary]
   path = /media/pi/Secondary
   browseable = yes
   writable = yes

[Videos]
   path = /media/pi/Videos
   browseable = yes
   writable = yes

[Temps]
   path = /media/pi/Temps
   browseable = yes
   writable = yes
```

**Screenshot:**  
![PI2-05](./screenshots/PI2-05_Pi_EditSmbConf_AllShares.png)

---

# **Step 6 — Restart Samba Services**

```bash
sudo systemctl restart smbd nmbd
sudo systemctl status smbd
```

**Screenshot:**  
![PI2-06](./screenshots/PI2-06_Pi_SambaService_Restart.png)

---

# **Step 7 — Create Samba User**

```bash
sudo smbpasswd -a pi
```

**Screenshot:**  
![PI2-07](./screenshots/PI2-07_Pi_CreateSambaUser.png)

---

# **Step 8 — macOS Finder: View All Shares**

Using Finder → Go → Connect to Server:

```
smb://<your Pi IP>
```

**Screenshot:**  
![PI2-08](./screenshots/PI2-08_Mac_Finder_AllShares.png)

---

# **Step 9 — macOS Create Folder Tests (Write Permission Test)**

These steps confirm macOS can write to each Samba share.

### **Primary1**
**Screenshot:**  
![PI2-09](./screenshots/PI2-09_Mac_CreateFolder_Primary1.png)

### **Secondary**
**Screenshot:**  
![PI2-10](./screenshots/PI2-10_Mac_CreateFolder_Secondary.png)

### **Videos**
**Screenshot:**  
![PI2-11](./screenshots/PI2-11_Mac_CreateFolder_Videos.png)

### **Temps**
**Screenshot:**  
![PI2-12](./screenshots/PI2-12_Mac_CreateFolder_Temps.png)

---

# **Step 10 — Windows 11: View All Shares**

Open File Explorer → Address Bar:

```
\\<Pi-IP>
```

**Screenshot:**  
![PI2-12W](./screenshots/PI2-12_Windows11_AllShares.png)

---

# **Step 11 — Raspberry Pi: Verify All macOS/Windows Folder Creations**

```bash
ls /media/pi/* -R
```

**Screenshot:**  
![PI2-13P](./screenshots/PI2-13_Pi_Verify_AllShares_Folders.png)

---

# **Step 12 — Windows Write Tests**

These steps confirm Windows can create files/folders on each share.

### **Primary1**
**Screenshot:**  
![PI2-13W](./screenshots/PI2-13_Windows11_WriteTest_Primary1.png)

### **Pi verifying Windows write (Primary1)**
**Screenshot:**  
![PI2-14](./screenshots/PI2-14_Pi_Verify_WindowsWrite_Primary1.png)

### **Secondary**
**Screenshot:**  
![PI2-15](./screenshots/PI2-15_Windows11_WriteTest_Secondary.png)

### **Temps**
**Screenshot:**  
![PI2-16](./screenshots/PI2-16_Windows11_WriteTest_Temps.png)

### **Videos**
**Screenshot:**  
![PI2-17](./screenshots/PI2-17_Windows11_WriteTest_Videos.png)

---

# ✅ Summary

You successfully:

- Installed and configured Samba  
- Added full read/write shares  
- Verified macOS read/write functionality  
- Verified Windows 11 read/write functionality  
- Confirmed file creation from both OS types on the Pi  

This Pi is now a fully working Samba file server.

