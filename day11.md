🟢 **Day X: Deploy Java Application on Tomcat 🚀**

---

📌 **Task Details (As Given)**  
The Nautilus application development team completed a Java-based application and decided to deploy it on Tomcat. The requirements were:

- Install Tomcat on App Server 3  
- Configure Tomcat to run on port `5002`  
- Deploy `ROOT.war` from Jump Host (`/tmp`)  
- Ensure application is accessible on base URL  
- Validate using: `curl http://stapp03:5002`  

---

🤔 **What is Required?**  
- Install and configure Tomcat  
- Modify default port from `8080` to `5002`  
- Transfer WAR file from jump host  
- Deploy WAR file as ROOT application  
- Restart service and verify application  

---

🔐 **Why This is Important?**  
- Enables deployment of Java applications  
- Demonstrates real-world web server configuration  
- Ensures applications are accessible via correct ports  
- Teaches WAR deployment and service management  

---

🖥️ **Server Details**

- App Server 3 → `stapp03` → User: `banner`  
- Jump Host → `jump-host` → User: `thor`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server 3**
```bash
ssh banner@stapp03
```

**2️⃣ Install Tomcat**
```bash
sudo yum install -y tomcat
```

**3️⃣ Configure Tomcat Port**
```bash
sudo vi /etc/tomcat/server.xml
```
Update:
```bash
<Connector port="5002" protocol="HTTP/1.1"
```

**4️⃣ Start and Enable Tomcat**
```bash
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

**5️⃣ Copy WAR File from Jump Host**
```bash
ssh thor@jump-host
scp /tmp/ROOT.war banner@stapp03:/tmp/
```

**6️⃣ Deploy WAR File**
```bash
ssh banner@stapp03
sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
```

**7️⃣ Restart Tomcat**
```bash
sudo systemctl restart tomcat
```
---

**▶️ Verification**

```bash
curl http://localhost:5002
curl http://stapp03:5002
```
Expected Output:
  GNU nano 8.6                                    day11.md                                     Modified
sudo systemctl enable tomcat
```

**5️⃣ Copy WAR File from Jump Host**
```bash
ssh thor@jump-host
scp /tmp/ROOT.war banner@stapp03:/tmp/
```

**6️⃣ Deploy WAR File**
```bash
ssh banner@stapp03
sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
```

**7️⃣ Restart Tomcat**
```bash
sudo systemctl restart tomcat
```
---

**▶️ Verification**

```bash
curl http://localhost:5002
curl http://stapp03:5002
```
Expected Output:
```bash
<h2>Welcome to xFusionCorp Industries!</h2>
```

---

**How It Works**

- Tomcat serves Java applications via WAR files
- ROOT.war ensures app loads on base URL
- Port change allows custom access configuration
- Restart applies configuration changes

---

**⚠️ Common Mistakes / Things That Can Go Wrong**

- Forgetting to change port from 8080 ❌
- Not restarting Tomcat after config change ❌
- Deploying WAR with wrong name (must be ROOT.war) ❌
- Copying WAR to wrong directory ❌
- Testing wrong URL (using /app instead of base URL) ❌
- Firewall or service not running ❌

---

**Final Status**

- Tomcat installed successfully ✅
- Port configured to 5002 ✅
- WAR file deployed correctly ✅
- Application accessible via base URL ✅
- Service verified using curl ✅
- Task completed 🚀

---
