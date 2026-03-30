🟢 **Day 07: Linux SSH Authentication**

---

📌 **Task Details (As Given)**  
The system admins team of `xFusionCorp Industries` has set up some scripts on `jump host` that run on regular intervals and perform operations on all app servers in `Stratos Datacenter`. To make these scripts work properly we need to make sure the `thor` user on jump host has password-less SSH access to all app servers through their respective sudo users (i.e `tony` for app server 1). Based on the requirements, perform the following:

Set up a password-less authentication from user `thor` on jump host to all app servers through their respective sudo users

---

🤔 **What is Required?**  
- Generate SSH key for user `thor`  
- Copy public key to all app servers  
- Enable password-less login  
- Configure access for:
  - `stapp01` → user `tony`
  - `stapp02` → user `steve`
  - `stapp03` → user `banner`

---

🔐 **Why This is Important?**  
- Enables automated script execution  
- Eliminates need for manual password entry  
- Improves efficiency in multi-server environments  
- Essential for DevOps and automation workflows  

---

🖥️ **Server Details**

- Jump Host → User: `thor`  
- `stapp01` → User: `tony`  
- `stapp02` → User: `steve`  
- `stapp03` → User: `banner`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Jump Host**
```bash
ssh thor@jump-host
```

**2️⃣ Generate SSH Key**
```bash
ssh-keygen -t rsa -b 2048
```
Press Enter for all prompts (no passphrase).


**3️⃣ Copy SSH Key to App Servers**
```bash
ssh-copy-id tony@stapp01

ssh-copy-id steve@stapp02

ssh-copy-id banner@stapp03
```

---

**▶️ Verification**
```bash
ssh tony@stapp01

ssh steve@stapp02

ssh banner@stapp03
```
Expected:
✔ Login without password

---

**How It Works**

- SSH key pair is generated on jump host
- Public key is copied to remote servers
- Stored in ~/.ssh/authorized_keys
- SSH authenticates using key instead of password

---

**⚠️ Common Mistakes**

- Not generating SSH key
- Entering wrong server credentials
- Using wrong user
- Permission issues in .ssh directory

---

**Final Status**

- SSH key generated on jump host ✅
- Keys copied to all app servers ✅
- Password-less SSH working successfully ✅
- Automation ready across servers ✅
- Task completed 🎯

---
