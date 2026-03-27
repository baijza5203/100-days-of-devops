🟢 **Day 03: Secure Root SSH Access 🔐🚫**

---

📌 **Task Details (As Given)**  
Following security audits, the `xFusionCorp Industries` security team has rolled out new protocols, including the restriction of direct root SSH login.

Your task is to disable direct SSH root login on all app servers within the `Stratos Datacenter`.

---

🤔 **What is Required?**  
- Modify SSH configuration  
- Disable root login access  
- Apply changes on:
  - App Server 1 (`stapp01`)
  - App Server 2 (`stapp02`)
  - App Server 3 (`stapp03`)

---

🔐 **Why This is Important?**  
- Prevents direct root access over SSH  
- Reduces risk of brute-force attacks  
- Enforces login via normal users + sudo  
- Improves overall system security  

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

**2️⃣ Open SSH Configuration File**
```bash
sudo nano /etc/ssh/sshd_config
```

**3️⃣ Update Root Login Setting**
Find the line:
```bash
#PermitRootLogin prohibit-password
```
Change it to:
```bash
PermitRootLogin no
```

- Remove #
- Ensure no duplicate entries exist

**4️⃣ Save and Exit**
- Press Ctrl + O → Enter
- Press Ctrl + X

**5️⃣ Restart SSH Service**
```bash
sudo systemctl restart sshd
```

**Repeat on All Servers**

- stapp01
- stapp02
- stapp03

**▶️ Verification**
```bash
ssh root@stapp01
```

Expected Output:
```bash
Permission denied
```

---

**How It Works**

- sshd_config controls SSH behavior
- PermitRootLogin no disables root login
- Restarting SSH applies the configuration

---

**⚠️ Common Mistakes**

- Forgetting to restart SSH service
- Leaving line commented (#PermitRootLogin)
- Multiple conflicting entries
- Editing wrong file (ssh_config instead of sshd_config)

---

**Final Status**

- Root SSH login disabled on all app servers ✅
- Secure access enforced via sudo users ✅
- Configuration verified successfully ✅
- Task completed 🎯

---
