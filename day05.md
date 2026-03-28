🟢 **Day 05: SElinux Installation and Configuration 🔐⚙️**

---

📌 **Task Details (As GIven)**  
Following a security audit, the xFusionCorp Industries security team has opted to enhance application and server security with SELinux. To initiate testing, the following requirements have been established for App server 2 in the Stratos Datacenter:



Install the required SELinux packages.

Permanently disable SELinux for the time being; it will be re-enabled after necessary configuration changes.

No need to reboot the server, as a scheduled maintenance reboot is already planned for tonight.

Disregard the current status of SELinux via the command line; the final status after the reboot should be disabled.

---

🤔 **What is Required?**  
- Install SELinux-related packages  
- Modify SELinux configuration  
- Disable SELinux permanently  
- Perform task on App Server 2 (`stapp02`)  

---

🔐 **Why This is Important?**  
- SELinux enhances system security through access control  
- Temporary disabling may be required for testing/configuration  
- Ensures controlled environment before re-enabling security policies  

---

🖥️ **Server Details**

- Hostname: `stapp02`  
- User: `steve`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Server**
```bash
ssh steve@stapp02
```

**2️⃣ Install SELinux Packages**
```bash
sudo yum install -y selinux-policy selinux-policy-targeted policycoreutils
```

**3️⃣ Open SELinux Configuration File**
```bash
sudo nano /etc/selinux/config
```

**4️⃣ Disable SELinux Permanently**
Find:
```bash
SELINUX=enforcing
```
Change to:
```bash
SELINUX=disabled
```

**5️⃣ Save and Exit**

- Press Ctrl + O → Enter
- Press Ctrl + X

---

**▶️ Verification**

```bash
cat /etc/selinux/config
```
Expected Output:
```bash
SELINUX=disabled
```
---

**How It Works**

- SELinux configuration is controlled via /etc/selinux/config
- Setting SELINUX=disabled ensures SELinux is turned off after reboot
- No immediate effect without reboot

---

**⚠️ Important Notes**

- No need to run setenforce 0
- No reboot required now
- Changes will apply after scheduled reboot

---

**⚠️ Common Mistakes**

- Forgetting to install required packages
- Editing wrong file
- Using incorrect value (disable instead of disabled)
- Expecting immediate effect without reboot

---

**Final Status**

- SELinux packages installed ✅
- SELinux permanently disabled ✅
- Configuration verified ✅
- Task completed 🎯

---
