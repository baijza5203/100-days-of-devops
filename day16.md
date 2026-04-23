🟢 **Day 16: Day 16: Install and Configure Nginx as an LBR ⚖️**

---

📌 **Task Details (As Given)**  
The Nautilus production support team observed increased traffic causing performance degradation. To resolve this, the application needed to be deployed on a high availability stack using a Load Balancer (LBR).

The task was to configure the LBR server (stlb01) to distribute traffic across multiple application servers.

---

🤔 **What is Required?**  
- Install Nginx on LBR  
- Configure load balancing using all app servers  
- Use ONLY /etc/nginx/nginx.conf  
- Do NOT modify Apache ports on app servers  
- Ensure Apache is running  
- Verify access using:
curl http://stlb01:80  

---

🔐 **Why This is Important?**  
- Distributes traffic across multiple servers  
- Improves performance and scalability  
- Prevents single point of failure  
- Core concept in production systems  

---

🖥️ **Server Details**

- App Server 1 → stapp01 → User: tony  
- App Server 2 → stapp02 → User: steve  
- App Server 3 → stapp03 → User: banner  
- Load Balancer → stlb01 → User: loki  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Load Balancer**
ssh loki@stlb01

---

**2️⃣ Install Nginx**
sudo yum install -y nginx

---

**3️⃣ Identify Apache Port (CRITICAL STEP)**
ssh tony@stapp01  
sudo ss -tulnp | grep httpd  

Expected:
*:8083  

---

**4️⃣ Configure Nginx Load Balancer**
sudo vi /etc/nginx/nginx.conf  

Replace content with:

events {}

http {

    upstream backend {
        server stapp01:8083;
        server stapp02:8083;
        server stapp03:8083;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://backend;
        }
    }

}

---

**5️⃣ Test Configuration**
sudo nginx -t  

Expected:
syntax is ok  
test is successful  

---

**6️⃣ Start & Enable Nginx**
sudo systemctl restart nginx  
sudo systemctl enable nginx  

---

▶️ **Verification**
curl http://stlb01:80  

Expected Output:
Welcome to xFusionCorp Industries!  

---

🧠 **How It Works**

- Nginx listens on port 80 (entry point)  
- Requests are forwarded to backend servers  
- Load balancing distributes traffic across:  
  stapp01:8083  
  stapp02:8083  
  stapp03:8083  
- Apache serves the application response  

---

🐛 **Debugging Journey**

- Initially assumed Apache was on port 80 ❌  
- Tried port 8082 → got 502 Bad Gateway ❌  
- Tried using container IPs (10.244.x.x) ❌  
- Modified /etc/hosts unnecessarily ❌  
- Finally checked using:
  ss -tulnp | grep httpd  

→ Found correct port: 8083 ✅  

---

⚠️ **Common Mistakes**

- Assuming Apache runs on port 80 ❌  
- Not checking actual service port ❌  
- Using wrong backend port ❌  
- Editing wrong nginx config ❌  
- Not restarting nginx ❌  
- Using container IPs ❌  
- Changing Apache config (not allowed) ❌  

---

💡 **Key Learnings**

- Always verify ports using:
  ss -tulnp  

- Load balancer port ≠ backend port  
- Follow task constraints strictly  
- Debug step-by-step (connectivity → config → service)  

---

✅ **Final Status**

- Nginx installed and configured ✅  
- Load balancing working correctly ✅  
- Apache unchanged (as required) ✅  
- Backend connectivity verified ✅  
- Website accessible via LBR ✅  
- Task completed successfully 🚀  

---
