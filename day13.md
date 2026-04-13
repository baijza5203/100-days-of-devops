🟢 **Day 13:  IPtables Installation And Configuration**

---

📌 **Task Details (As Given)**  
A website is running on Nautilus infrastructure, and Apache is configured on port `3000`. The security team identified that this port is open to all hosts due to lack of firewall configuration. To enhance security, the following tasks were required:

- Install iptables on all app servers  
- Block incoming traffic on port `3000`  
- Allow access only from Load Balancer (LBR) host  
- Ensure rules persist after reboot  

---

🤔 **What is Required?**  
- Install iptables and its services  
- Configure firewall rules to restrict access  
- Allow only LBR host to access port `3000`  
- Save rules permanently  

---

🔐 **Why This is Important?**  
- Prevents unauthorized access to application port  
- Ensures controlled traffic via Load Balancer  
- Adds a critical security layer to servers  
- Demonstrates firewall configuration and persistence  

---

🖥️ **Server Details**

- App Server 1 → `stapp01` → User: `tony`  
- App Server 2 → `stapp02` → User: `steve`  
- App Server 3 → `stapp03` → User: `banner`  
- Load Balancer → `stlb01` → IP: `10.244.234.234`  

---

⚙️ **Implementation Steps (Performed on All App Servers)**

**1️⃣ Connect to App Server**
```bash
ssh <user>@stapp0X
```

**2️⃣ Install iptables**
```bash
sudo yum install -y iptables iptables-services
```

**3️⃣ Start and Enable iptables**
```bash
sudo systemctl start iptables
sudo systemctl enable iptables
```

**4️⃣ Flush Existing Rules (Clean Setup)**
```bash
sudo iptables -F
```

**5️⃣ Allow Access from Load Balancer (IMPORTANT FIRST RULE)**
```bash
sudo iptables -A INPUT -p tcp --dport 3000 -s 10.244.234.234 -j ACCEPT
```

**6️⃣ Block Access for All Other Sources**
```bash
sudo iptables -A INPUT -p tcp --dport 3000 -j DROP
```

**7️⃣ Save Rules for Persistence (RHEL 9 Method)**
```bash
sudo iptables-save | sudo tee /etc/sysconfig/iptables
```

**8️⃣ Restart iptables Service**
```bash
sudo systemctl restart iptables
```

---

**▶️ Verification**
```bash
sudo iptables -L -n
```
Expected:
```bash
ACCEPT tcp -- 10.244.234.234 0.0.0.0/0 tcp dpt:3000
DROP   tcp -- 0.0.0.0/0      0.0.0.0/0 tcp dpt:3000
```

---

** How It Works**

- iptables filters incoming traffic based on defined rules
- ACCEPT rule allows only Load Balancer traffic
- DROP rule blocks all other sources
- Saving rules ensures persistence after reboot

---

**⚠️ Common Mistakes / Things That Can Go Wrong**

- Using hostname instead of IP address ❌
- Adding DROP rule before ACCEPT (wrong rule order) ❌
- Not installing iptables-services ❌
- Forgetting to save rules (lost after reboot) ❌
- Applying rules on only one server ❌
- Using deprecated service iptables save command ❌

---

** Final Status**

- iptables installed on all app servers ✅
- Port 3000 restricted successfully ✅
- Access allowed only from Load Balancer ✅
- Rules saved and persistent after reboot ✅
- Task completed 🚀

---
