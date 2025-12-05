# 🏗️ Raspberry Pi Lab 2 — File Server with Samba

A complete walkthrough of configuring a Raspberry Pi 4 as a network-accessible file server using Samba.

---

## 📌 Overview

This lab configures your Raspberry Pi as a network file server using **Samba**, enabling shared folder access from Windows, macOS, and Linux.

---

## 📂 Repository Structure

```
lab-2-samba-file-server/
│── README.md
└── screenshots/
    RPI2-01_Terminal_Update_Upgrade.png
    RPI2-02_lsblk_List_Drives.png
    RPI2-03_lsblk_Mounted_Drives.png
    RPI2-04_Backup_fstab_Before_Edit.png
    RPI2-05_Edit_fstab_With_Mount_Entries.png
    RPI2-06_Mount_Test_Success.png
    RPI2-07_Apply_Permissions_Primary1.png
    RPI2-08_Apply_Permissions_Secondary_Videos.png
    RPI2-09_Install_Samba.png
    RPI2-10_Backup_smb_conf.png
    RPI2-11_Edit_smb_conf_Shares.png
    RPI2-12_Testparm_No_Errors.png
    RPI2-13_Create_Samba_User.png
    RPI2-14_Restart_Samba_Services.png
    RPI2-15_Firewall_Allow_Samba_or_Skip.png
    RPI2-16_Windows_Run_SMB_Path.png
    RPI2-17_Windows_Enter_Network_Credentials.png
    RPI2-18_Windows_Share_Opened.png
    RPI2-19_macOS_Connect_To_Server.png
    RPI2-20_macOS_Share_Mounted_Finder.png
```

---

# ✅ Step-by-Step Guide (Screenshots Included in Each Step)

---

# **Step 1 — Update & Upgrade**

```bash
sudo apt update && sudo apt upgrade -y
```

**Screenshot:**  
![RPI2-01](./screenshots/RPI2-01_Terminal_Update_Upgrade.png)

---

# **Step 2 — Identify Attached Drives**

Run:

```bash
lsblk -f
```

**Screenshot:**  
![RPI2-02](./screenshots/RPI2-02_lsblk_List_Drives.png)

If auto-mounted:

**Screenshot:**  
![RPI2-03](./screenshots/RPI2-03_lsblk_Mounted_Drives.png)

---

# **Step 3 — Configure Persistent Mounts (fstab)**

## 3.1 Backup fstab

```bash
sudo cp /etc/fstab /etc/fstab.backup
```

**Screenshot:**  
![RPI2-04](./screenshots/RPI2-04_Backup_fstab_Before_Edit.png)

---

## 3.2 Edit fstab

```bash
sudo nano /etc/fstab
```

Add:

```
UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  /media/pi/Primary1   ext4  defaults,uid=1000,gid=1000,umask=002  0 2
UUID=yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy  /media/pi/Secondary  ext4  defaults,uid=1000,gid=1000,umask=002  0 2
UUID=zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz  /media/pi/Videos     ext4  defaults,uid=1000,gid=1000,umask=002  0 2
```

**Screenshot:**  
![RPI2-05](./screenshots/RPI2-05_Edit_fstab_With_Mount_Entries.png)

---

## 3.3 Test mounts

```bash
sudo mount -a
lsblk -f
df -h | grep /media/pi
```

**Screenshot:**  
![RPI2-06](./screenshots/RPI2-06_Mount_Test_Success.png)

---

# **Step 4 — Set Folder Permissions**

```bash
sudo chown -R pi:pi /media/pi/Primary1
sudo chmod -R 775 /media/pi/Primary1

sudo chown -R pi:pi /media/pi/Secondary
sudo chmod -R 775 /media/pi/Secondary

sudo chown -R pi:pi /media/pi/Videos
sudo chmod -R 775 /media/pi/Videos
```

**Screenshots:**  
Primary1 → ![RPI2-07](./screenshots/RPI2-07_Apply_Permissions_Primary1.png)  
Secondary + Videos → ![RPI2-08](./screenshots/RPI2-08_Apply_Permissions_Secondary_Videos.png)

---

# **Step 5 — Install Samba**

```bash
sudo apt install samba -y
```

**Screenshot:**  
![RPI2-09](./screenshots/RPI2-09_Install_Samba.png)

---

# **Step 6 — Backup & Configure smb.conf**

## 6.1 Backup:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
```

**Screenshot:**  
![RPI2-10](./screenshots/RPI2-10_Backup_smb_conf.png)

---

## 6.2 Edit smb.conf

```bash
sudo nano /etc/samba/smb.conf
```

Add:

```
[Primary1]
   path = /media/pi/Primary1
   browseable = yes
   writable = yes
   valid users = @smbusers

[Secondary]
   path = /media/pi/Secondary
   browseable = yes
   writable = yes
   valid users = @smbusers

[Videos]
   path = /media/pi/Videos
   browseable = yes
   writable = yes
   valid users = @smbusers
```

**Screenshot:**  
![RPI2-11](./screenshots/RPI2-11_Edit_smb_conf_Shares.png)

---

# **Step 7 — Create Samba Group + User**

```bash
sudo groupadd smbusers
sudo usermod -aG smbusers pi
sudo smbpasswd -a pi
```

**Screenshot:**  
![RPI2-13](./screenshots/RPI2-13_Create_Samba_User.png)

---

# **Step 8 — Validate Samba Config**

## 8.1 Test:

```bash
testparm
```

**Screenshot:**  
![RPI2-12](./screenshots/RPI2-12_Testparm_No_Errors.png)

---

## 8.2 Restart Samba

```bash
sudo systemctl restart smbd nmbd
sudo systemctl status smbd
```

**Screenshot:**  
![RPI2-14](./screenshots/RPI2-14_Restart_Samba_Services.png)

---

# **Step 9 — Optional Firewall Rules**

```bash
sudo ufw allow samba
sudo ufw status
```

**Screenshot:**  
![RPI2-15](./screenshots/RPI2-15_Firewall_Allow_Samba_or_Skip.png)

---

# **Step 10 — Connect from Windows**

Open **Run (Win+R)**:

```
\\192.168.x.x
```

**Screenshot:**  
![RPI2-16](./screenshots/RPI2-16_Windows_Run_SMB_Path.png)

Enter credentials:

**Screenshot:**  
![RPI2-17](./screenshots/RPI2-17_Windows_Enter_Network_Credentials.png)

Open a share:

**Screenshot:**  
![RPI2-18](./screenshots/RPI2-18_Windows_Share_Opened.png)

---

# **Step 11 — Connect from macOS**

Finder → Go → Connect to Server:

```
smb://192.168.x.x
```

**Screenshots:**  
Connect window → ![RPI2-19](./screenshots/RPI2-19_macOS_Connect_To_Server.png)  
Mounted share in Finder → ![RPI2-20](./screenshots/RPI2-20_macOS_Share_Mounted_Finder.png)

---

# ✅ Verification Checklist

- Drives mount automatically via fstab  
- Permissions set correctly  
- Samba user created  
- `testparm` shows no errors  
- Windows/macOS clients can read/write  
- All **20 screenshots** completed  

---

# 🧹 Troubleshooting

- Check Samba status:
```bash
sudo systemctl status smbd
```

- Verify mounts:
```bash
df -h | grep /media/pi
```

- Fix permissions:
```bash
sudo chown -R pi:pi /media/pi/*
sudo chmod -R 775 /media/pi/*
```

---

# 🎉 Lab Complete
Your Raspberry Pi is now a functional Samba file server.

