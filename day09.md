🟢 **Day 09: MariaDB Troubleshooting**

---

📌 **Task Details (As Given)** 
There is a critical issue going on with the Nautilus application in Stratos DC. 
The production support team identified that the application is unable to connect to the database. After 
digging into the issue, the team found that mariadb service is down on the database server. Look into the 
issue and fix the same

---

🤔 **What is Required?**  
- Identify why MariaDB is not running  
- Troubleshoot the issue  
- Reinitialize database if required  
- Start and enable MariaDB service  
- Restore application connectivity  

---

🔐 **Why This is Important?**  
- Applications depend on database availability  
- Database downtime impacts production systems  
- Ensures reliability and uptime  
- Demonstrates real-world troubleshooting skills  

---

🖥️ **Server Details**

- Database Server → `stdb01`  
- User → `peter`  

---

⚙️ **Implementation Steps**

**1 Connect to Database Server**
```bash
ssh peter@stdb01
```

**2 Check MariaDB Service Status**
```bash
sudo systemctl status mariadb
```

**3 Stop MariaDB (if needed)**
```bash
sudo systemctl stop mariadb
```

**4 Clean Data Directory**
```bash
sudo rm -rf /var/lib/mysql/*
```

**5 Reinitialize Database**
```bash
sudo mariadb-install-db --user=mysql --datadir=/var/lib/mysql
```

**6 Fix Permissions**
```bash
sudo chown -R mysql:mysql /var/lib/mysql
```

**7 Fix Runtime Directory**
```bash
sudo mkdir -p /var/run/mariadb
sudo chown -R mysql:mysql /var/run/mariadb
sudo chmod 755 /var/run/mariadb
```

**8 Restore SELinux Context**
```bash
sudo restorecon -Rv /var/lib/mysql
```

**9 Start MariaDB Service**
```bash
sudo systemctl start mariadb
```

**10 Enable MariaDB Service**
```bash
sudo systemctl enable mariadb
```

---

**▶️ Verification**
```bash
sudo systemctl status mariadb
```
Expected Output:
```bash
active (running)
```
Optional:
```bash
mysql
```

----

**How It Works**

- MariaDB requires a valid data directory to start
- Missing or corrupted data prevents service startup
- Proper permissions ensure access by mysql user
- Runtime directory is needed for socket creation
- SELinux context ensures correct security labeling

---

**⚠️ Common Mistakes**

- Not cleaning /var/lib/mysql before reinitializing
- Skipping permission fixes
- Ignoring runtime directory
- Running commands on wrong server

---

**Final Status**

- Issue identified successfully ✅
- Data directory cleaned ✅
- Database reinitialized ✅
- Permissions fixed ✅
- MariaDB service started ✅
- Service enabled ✅
- Task completed 🎯

---
