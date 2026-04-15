🟢 **Day 15: Deploy Nginx with SSL Configuration 🔐**

---

📌 **Task Details (As Given)**  
The system admins team needed to prepare App Server 1 for application deployment. The requirements included:

- Install and configure Nginx  
- Deploy a self-signed SSL certificate and key  
- Create a basic web page  
- Verify access using HTTPS from jump host  

---

🤔 **What is Required?**  
- Install and start Nginx  
- Configure SSL using provided certificate and key  
- Set up a web page with required content  
- Validate HTTPS access using curl  

---

🔐 **Why This is Important?**  
- Enables secure communication using HTTPS  
- Prepares server for production deployments  
- Demonstrates web server and SSL configuration  
- Ensures secure access to applications  

---

🖥️ **Server Details**

- App Server 1 → `stapp01` → User: `tony`  
- Jump Host → `jump-host` → User: `thor`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server 1**
```bash
ssh tony@stapp01
```

**2️⃣ Install Nginx**
```bash
sudo yum install -y nginx
```

**3️⃣ Start and Enable Nginx**
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

**4️⃣ Deploy SSL Certificates**
```bash
sudo mkdir -p /etc/nginx/ssl
sudo cp /tmp/nautilus.crt /etc/nginx/ssl/
sudo cp /tmp/nautilus.key /etc/nginx/ssl/
```

**5️⃣ Configure Nginx for HTTPS**
```bash
sudo vi /etc/nginx/nginx.conf
```
Add Server Block:
```bash
server {
    listen 443 ssl;
    server_name stapp01;

    ssl_certificate /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}
```

**6️⃣ Create Web Page**
```bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
```

**7️⃣ Test Configuration**
```bash
sudo nginx -t
```
Expected:
```bash
syntax is ok
test is successful
```

**8️⃣ Restart Nginx**
```bash
sudo systemctl restart nginx
```

---

**▶️ Verification**
```bash
ssh thor@jump-host
curl -Ik https://stapp01
```
Expected Output:
```bash
HTTP/1.1 200 OK
```

---

** How It Works**

- Nginx serves web content over HTTPS
- SSL certificates enable encrypted communication
- ROOT directory serves index.html
- Curl verifies server response and SSL configuration

---

**⚠️ Common Mistakes / Things That Can Go Wrong**

- Incorrect certificate path ❌
- Missing SSL configuration ❌
- Not restarting nginx after changes ❌
- Using HTTP instead of HTTPS ❌
- Not using -k for self-signed certificate ❌
- Typo in config file ❌

---

** Final Status**

- Nginx installed and running ✅
- SSL configured successfully ✅
- Web page created and served ✅
- HTTPS access verified from jump host ✅
- Task completed 🚀

---





























