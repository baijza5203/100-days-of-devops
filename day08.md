🟢 **Day 08: Install Ansible⚙️**

---

📌 **Task Details (As Given)**  
During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.

Install ansible version 4.8.0 on Jump host using pip3 only. Make sure Ansible binary is available globally on this system, i.e all users on this system are able to run Ansible commands.

---

🤔 **What is Required?**  
- Install `pip3` (if not available)  
- Install Ansible version `4.8.0` using pip3  
- Ensure global accessibility of Ansible  
- Perform task on Jump Host  

---

🔐 **Why This is Important?**  
- Ansible is used for automation and configuration management  
- Enables centralized control over multiple servers  
- Simplifies deployment and operational tasks  
- Requires minimal setup compared to other tools  

---

🖥️ **Server Details**

- Jump Host → User: `thor`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Jump Host**
```bash
ssh thor@jump-host
```

**2️⃣ Install pip3 (if not already installed)**
```bash
sudo yum install -y python3-pip
```

**3️⃣ Install Ansible Version 4.8.0**
```bash
sudo pip3 install ansible==4.8.0
```

**4️⃣ Ensure Ansible is Globally Accessible**
Check installation path:
```bash
which ansible
```

If needed, add to PATH:
```bash
echo 'export PATH=$PATH:/usr/local/bin' | sudo tee -a /etc/profile
source /etc/profile
```
---

**▶️ Verification**
```bash
ansible --version
```
Expected Output should include:
```bash
ansible 4.8.0
```
---

**How It Works**

- pip3 installs Python-based packages globally
- Ansible binaries are placed in /usr/local/bin
- Adding to PATH ensures accessibility for all users

---

**⚠️ Common Mistakes**

- Installing Ansible using yum instead of pip3
- Installing incorrect version
- Using pip instead of pip3
- Not verifying installation

---

**🎉 Final Status

- pip3 installed successfully ✅
- Ansible 4.8.0 installed via pip3 ✅
- Ansible accessible globally ✅
- Installation verified ✅
- Task completed

---
