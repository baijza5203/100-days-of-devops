🟢 **Day 14: Linux Process Troubleshooting**

---

📌 **Task Details (As Given)**  
A monitoring system reported Apache service unavailability on one of the app servers in Stratos DC. The task was to:

- Identify the faulty app server  
- Fix Apache service  
- Ensure Apache runs on all app servers  
- Configure Apache to run on port `3004` on all servers  

---

🤔 **What is Required?**  
- Check Apache status on all app servers  
- Identify and fix the faulty server  
- Configure Apache port correctly  
- Restart and verify service  

---

🔐 **Why This is Important?**  
- Ensures application availability  
- Fixes service downtime issues  
- Standardizes configuration across servers  
- Demonstrates troubleshooting skills  

---

🖥️ **Server Details**

- App Server 1 → `stapp01` → User: `tony`  
- App Server 2 → `stapp02` → User: `steve`  
- App Server 3 → `stapp03` → User: `banner`  

---

⚙️ **Implementation Steps**

**1️⃣ Identify Faulty Server**
```bash
sudo systemctl status httpd
```
Found:
- stapp01 → Apache service failed ❌


**2️⃣ Analyze Error**
```bash
sudo systemctl status httpd
```
Error:
```bash
Address already in use
```

**3️⃣ Root Cause**
- Port conflict on 3004
- Stale Apache processes were running
- Service state inconsistent


**4️⃣ Fix Service (Clean Restart)**
```bash
sudo systemctl stop httpd
sudo pkill -9 httpd
sudo systemctl start httpd
sudo systemctl enable httpd
```

**5️⃣ Configure Apache Port (All Servers)**
```bash
sudo vi /etc/httpd/conf/httpd.conf
```
Update:
```bash
Listen 3004
```

**6️⃣ Validate Configuration**
```bash
sudo apachectl configtest
```
Expected:
```bash
Syntax OK
```

**7️⃣ Restart Apache**
```bash
sudo systemctl restart httpd
```

---

**▶️ Verification**
```bash
sudo systemctl status httpd
```
Expected:
```bash
active (running)
```
```bash
ss -tulnp | grep 3004
```
Expected:
```bash
*:3004
```

---

** How it Works**

- Apache listens on configured port
- Port conflict prevents service startup
- Killing stale processes frees the port
- Restart ensures clean servic

---

**⚠️ Common Mistakes / Things That Can Go Wrong**

- Not checking all app servers ❌
- Leaving Apache on default port 80 ❌
- Not restarting service after config change ❌
- Ignoring port conflicts ❌
- Not killing stale processes ❌
- Incorrect Listen directive (127.0.0.1 instead of global) ❌

---

** Final Status**

- Faulty server identified (stapp01) ✅
- Apache service fixed successfully ✅
- Port configured to 3004 on all servers ✅
- Service running on all app servers ✅
- Task completed 🚀

---

