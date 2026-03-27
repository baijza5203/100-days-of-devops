🟢 **Day 04: Grant Execute Permission to Script ⚙️📜**

---

📌 **Task Details**  
Grant executable permissions to the `/tmp/xfusioncorp.sh` script on **App Server 1**.  
Ensure that **all users** can execute the script.

---

🤔 **What is Required?**  
- Modify file permissions  
- Make the script executable  
- Allow execution for all users  
- Perform task on App Server 1 (`stapp01`)

---

🔐 **Why This is Important?**  
- Scripts must have execute permission to run  
- Required for automation tools and scheduled jobs  
- Ensures accessibility for all users  
- Supports system-wide operations  

---

🖥️ **Server Details**

- Hostname: `stapp01`  
- User: `tony`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Server**
```bash
ssh tony@stapp01
```

**2️⃣ Grant Execute Permission to All Users**
```bash
sudo chmod a+x /tmp/xfusioncorp.sh
```
---

**Explanation**

- chmod → Changes file permissions
- a+x → Adds execute permission for:
	- User (owner)
	- Group
	- Others

---

**▶️ Verification**

```bash
ls -l /tmp/xfusioncorp.sh
```
Expected Output:
```bash
---x--x--x
```
✔ All users have execute permission

---

**Optional (Standard Permission Format)**

```bash
sudo chmod 755 /tmp/xfusioncorp.sh
```
Result:
```bash
-rwxr-xr-x
```

---

**⚠️ Common Mistakes**

- Forgetting sudo
- Giving wrong permissions
- Not verifying using ls -l
- Using incorrect file path

---

**Final Status**

- Script made executable ✅
- Execute permission granted to all users ✅
- Verified successfully ✅
- Task completed 🎯

---
