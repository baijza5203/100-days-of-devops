🟢 **Day 10: Website Backup Script 📦**

---

📌 **Task Details (As Given)**  
The production support team of xFusionCorp Industries is working on automating daily tasks. One requirement is to create a bash script named `news_backup.sh` on App Server 1. The script should:

- Create a zip archive of `/var/www/html/news`  
- Save it in `/backup/` on App Server 1  
- Copy the archive to `/backup/` on Nautilus Storage Server  
- Ensure passwordless transfer  
- Avoid using `sudo` inside the script  

---

🤔 **What is Required?**  
- Install `zip` package manually  
- Create `/scripts/news_backup.sh`  
- Archive the correct directory structure  
- Copy backup to storage server using `scp`  
- Configure passwordless SSH  
- Ensure script runs with normal user permissions  

---

🔐 **Why This is Important?**  
- Automates website backup process  
- Ensures data availability and recovery  
- Reduces manual effort and human error  
- Simulates real-world DevOps backup workflows  

---

🖥️ **Server Details**

- App Server 1 → `stapp01` → User: `tony`  
- Storage Server → `ststor01` → User: `natasha`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server**
```bash
ssh tony@stapp01
```
**2️⃣ Install zip (outside script)**
```bash
sudo yum install -y zip
```
**3️⃣ Setup passwordless SSH**
```bash
ssh-keygen -t rsa
ssh-copy-id natasha@ststor01
```
**4️⃣ Create scripts directory**
```bash
mkdir -p /scripts
```
**5️⃣ Create script**
```bash
vi /scripts/news_backup.sh
```
Script Content:
```bash
#!/bin/bash

SOURCE="/var/www/html/news"
DEST="/backup"
ARCHIVE="xfusioncorp_news.zip"
REMOTE_USER="natasha"
REMOTE_HOST="ststor01"
REMOTE_DIR="/backup"

# Remove old archive if exists
rm -f $DEST/$ARCHIVE

# Create archive
zip -r $DEST/$ARCHIVE $SOURCE

# Copy archive to storage server
scp $DEST/$ARCHIVE ${REMOTE_USER}@${REMOTE_HOST}:${REMOTE_DIR}

echo "Backup completed successfully"
```
**6️⃣ Make script executable**
```bash
chmod +x /scripts/news_backup.sh
```
**7️⃣ Run script**
```bash
/scripts/news_backup.sh
```

---

**▶️ Verification**
```bash
ls /backup/
unzip -l /backup/xfusioncorp_news.zip
ssh natasha@ststor01
ls /backup/
```

---

**How It Works**

- zip -r creates a compressed archive of the directory
- /backup acts as temporary storage
- scp transfers file securely to storage server
- SSH key authentication prevents password prompts

---

**⚠️ Common Mistakes / Things That Can Go Wrong**

- Zipping only contents instead of full directory (wrong structure) ❌
- Forgetting to install zip package ❌
- Not setting up passwordless SSH (script prompts for password) ❌
- Using sudo inside script (violates requirement) ❌
- Incorrect file paths (/var/www/html/news) ❌
- Script not executable ❌
- Old archive not removed, causing overwrite issues ❌
- Wrong remote user or hostname ❌
- Not verifying archive contents before submission ❌

---

**Final Status**

- Script created successfully ✅
- Archive generated with correct structure ✅
- Backup stored locally in /backup/ ✅
- Backup copied to storage server ✅
- Passwordless SSH configured ✅
- Task completed 🚀

---

