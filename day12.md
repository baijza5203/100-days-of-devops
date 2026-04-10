🟢 **Day 12:  Linux Network Services**

---

📌 **Task Details (As Given)**  
The monitoring tool reported that Apache service on App Server 1 was not reachable on port `3003`. The issue could be due to service failure, firewall, or other networking problems.

Requirements:

- Identify why Apache is not reachable on port `3003`  
- Fix the issue without modifying `index.html`  
- Ensure Apache is accessible from Jump Host  
- Validate using: `curl http://stapp01:3003`  

---

🤔 **What is Required?**  
- Troubleshoot Apache service failure  
- Identify port conflicts or misconfigurations  
- Ensure Apache runs on port `3003`  
- Resolve network-level access issues  
- Verify accessibility from another server  

---

🔐 **Why This is Important?**  
- Teaches real-world service troubleshooting  
- Demonstrates debugging of port conflicts  
- Builds understanding of networking layers  
- Helps diagnose “No route to host” errors  
- Strengthens Linux system administration skills  

---

🖥️ **Server Details**

- App Server 1 → `stapp01` → User: `tony`  
- Jump Host → `jump-host` → User: `thor`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server**

```bash
ssh tony@stapp01
```

---

**2️⃣ Check Apache Service Status**

```bash
sudo systemctl status httpd
```

---

**3️⃣ Attempt to Start Apache**

```bash
sudo systemctl start httpd
```

❌ Failed due to port conflict

---

**4️⃣ Identify Port Conflict**

```bash
sudo ss -tulnp | grep 3003
```

Output showed:

```
sendmail using port 3003
```

---

**5️⃣ Stop Conflicting Service**

```bash
sudo systemctl stop sendmail
sudo systemctl disable sendmail
```

---

**6️⃣ Start Apache Service**

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

---

**7️⃣ Verify Apache is Listening**

```bash
sudo ss -tulnp | grep 3003
```

Output:

```
httpd listening on *:3003
```

---

**8️⃣ Test Locally**

```bash
curl http://localhost:3003
```

✅ Worked locally

---

**9️⃣ Test from Jump Host**

```bash
ssh thor@jump-host
curl http://stapp01:3003
```

❌ Error: No route to host

---

**🔟 Fix Network-Level Access (iptables)**

```bash
sudo iptables -I INPUT -p tcp --dport 3003 -j ACCEPT
```

---

▶️ **Verification**

```bash
curl http://stapp01:3003
```

Expected Output:

```html
<h2>Welcome to xFusionCorp Industries!</h2>
```

---

🧠 **How It Works**

* Apache serves web content over configured ports  
* Port conflicts prevent services from starting  
* `sendmail` was occupying required port  
* iptables rules control external access  
* Allowing port enables communication between servers  

---

⚠️ **Common Mistakes / Things That Can Go Wrong**

* Apache not running ❌  
* Port already in use ❌  
* Wrong port configuration ❌  
* Forgetting to stop conflicting service ❌  
* Not checking listening ports ❌  
* Ignoring network-level errors ❌  
* Misinterpreting “No route to host” ❌  

---

🎉 **Final Status**

* Apache service started successfully ✅  
* Port conflict resolved ✅  
* Service listening on port 3003 ✅  
* Network access enabled ✅  
* Application reachable from jump host ✅  
* Task completed 🚀  

---
