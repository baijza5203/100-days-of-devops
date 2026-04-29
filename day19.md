🟢 **Day 19: Configure Apache to Host Multiple Websites on Custom Port 🌐**

---

📌 **Task Details (As Given)**  
xFusionCorp Industries plans to host two static websites on their infrastructure. The websites are still under development, but the server must be prepared in advance.

The task involves installing Apache, configuring it to run on a custom port, and deploying two websites so they can be accessed via specific URLs.

---

🤔 **What is Required?**  
- Install Apache (httpd)  
- Configure Apache to run on port 5000  
- Deploy two websites: beta and demo  
- Ensure access via:
  http://localhost:5000/beta/  
  http://localhost:5000/demo/  

---

🔐 **Why This is Important?**  
- Enables hosting multiple websites on a single server  
- Demonstrates custom port configuration  
- Prepares infrastructure before application deployment  
- Core concept in web server management  

---

🖥️ **Server Details**

- App Server 1 → stapp01 → User: tony  
- Jump Host → jump-host → User: thor  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server**
ssh tony@stapp01  

---

**2️⃣ Install Apache**
sudo yum install -y httpd  

---

**3️⃣ Configure Apache Port**
sudo vi /etc/httpd/conf/httpd.conf  

Find:
Listen 80  

Change to:
Listen 5000  

---

**4️⃣ Start and Enable Apache**
sudo systemctl start httpd  
sudo systemctl enable httpd  

---

**5️⃣ Copy Website Files from Jump Host**
scp -r thor@jump-host:/home/thor/beta/ /tmp/  
scp -r thor@jump-host:/home/thor/demo/ /tmp/  

---

**6️⃣ Move Files to Web Directory**
sudo cp -r /tmp/beta /var/www/html/  
sudo cp -r /tmp/demo /var/www/html/  

---

**7️⃣ Set Permissions**
sudo chown -R apache:apache /var/www/html/beta  
sudo chown -R apache:apache /var/www/html/demo  

---

**8️⃣ Restart Apache**
sudo systemctl restart httpd  

---

▶️ **Verification**

curl http://localhost:5000/beta/  
curl http://localhost:5000/demo/  

Expected Output:
- Beta site content  
- Demo site content  

---

🧠 **How It Works**

- Apache listens on port 5000 instead of default port 80  
- Default web root is /var/www/html  
- Subdirectories:
  /beta → accessible via /beta/  
  /demo → accessible via /demo/  
- Apache serves static content from these directories  

---

⚠️ **Common Mistakes**

- Forgetting to change port ❌  
- Not restarting Apache ❌  
- Using scp without -r for directories ❌  
- Incorrect file paths ❌  
- Wrong permissions ❌  
- Missing trailing slash in URL ❌  

---

💡 **Key Learnings**

- Apache can serve multiple sites via directory structure  
- Custom ports are commonly used in real environments  
- scp -r is required for copying directories  
- Always verify using curl  

---

✅ **Final Status**

- Apache installed and configured ✅  
- Custom port (5000) working ✅  
- Beta website deployed successfully ✅  
- Demo website deployed successfully ✅  
- Access verified via curl ✅  
- Task completed 🚀  

---
