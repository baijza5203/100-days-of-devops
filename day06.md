🟢 **Day 06: Configure Cron Job on Multiple Servers ⏰⚙️**

---

📌 **Task Details**  
Install `cronie` on all app servers, start the `crond` service, and configure a cron job for the root user to execute every 5 minutes.

---

🤔 **What is Required?**  
- Install `cronie` package  
- Start and enable `crond` service  
- Add cron job for root user  
- Execute task on:
  - App Server 1 (`stapp01`)
  - App Server 2 (`stapp02`)
  - App Server 3 (`stapp03`)

---

🔐 **Why This is Important?**  
- Automates repetitive system tasks  
- Reduces manual intervention  
- Ensures consistency across servers  
- Essential for backups, monitoring, and maintenance  

---

🖥️ **Server Details**

- `stapp01` → User: `tony`  
- `stapp02` → User: `steve`  
- `stapp03` → User: `banner`  

---

⚙️ **Implementation Steps (Performed on All App Servers)**

**1️⃣ Connect to Server**
```bash
ssh <user>@<server>
```
Example:
```bash
ssh tony@stapp01
```

**2️⃣ Install Cronie Package**
```bash
sudo yum install -y cronie
```

**3️⃣ Start and Enable crond Service**
```bash
sudo systemctl start crond
sudo systemctl enable crond
```

**4️⃣ Add Cron Job for Root User**
```bash
sudo crontab -e
```
Add the following line:
```bash
*/5 * * * * echo hello > /tmp/cron_text
```
---

**▶️ Verification**
Wait up to 5 minutes, then run:
```bash
cat /tmp/cron_text
```
Expected Output:
```bash
hello
```
---

**How It Works**

- cronie provides cron functionality
- crond service executes scheduled tasks
- */5 * * * * runs the job every 5 minutes
- Output is written to /tmp/cron_text

---

**⚠️ Important Notes**

- Cron jobs do not run immediately
- They execute at scheduled intervals (every 5 minutes here)
- Ensure the cron job is added for the root user

---

**⚠️ Common Mistakes**

- Forgetting to start crond service
- Not enabling the service
- Adding cron under wrong user
- Checking output too early
- Syntax errors in cron job

---

**Final Status**

- cronie installed on all servers ✅
- crond service running and enabled ✅
- Cron job added successfully ✅
- Output verified after execution ✅
- Task completed 🎯

---
