🟢 **Day 20: Configure Nginx with PHP-FPM (PHP 8.2) on Custom Port ⚙️**

---

📌 **Task Details (As Given)**  
The Nautilus application development team plans to deploy a PHP-based application on App Server 2. The infrastructure must be prepared with Nginx and PHP-FPM configured correctly to process PHP files.

Two files (index.php and info.php) are already placed under /var/www/html and must not be modified.

---

🤔 **What is Required?**  
- Install Nginx on stapp02  
- Configure Nginx to run on port 8091  
- Set document root to /var/www/html  
- Install PHP-FPM version 8.2  
- Configure PHP-FPM to use socket:
  /var/run/php-fpm/default.sock  
- Integrate Nginx with PHP-FPM  
- Verify using:
  curl http://stapp02:8091/index.php  

---

🔐 **Why This is Important?**  
- Enables execution of dynamic PHP applications  
- Demonstrates integration between web server and application runtime  
- Uses Unix socket for efficient communication  
- Reflects real-world production architecture  

---

🖥️ **Server Details**

- App Server 2 → stapp02 → User: steve  
- Jump Host → jump-host  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to App Server**
ssh steve@stapp02  

---

**2️⃣ Install Nginx**
sudo yum install -y nginx  

---

**3️⃣ Configure Nginx**
sudo nano /etc/nginx/nginx.conf  

Update server block:

server {
    listen 8091;
    listen [::]:8091;
    server_name _;

    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        root /var/www/html;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}

---

**4️⃣ Install PHP 8.2**
sudo yum module reset php -y  
sudo yum module enable php:8.2 -y  
sudo yum install -y php php-fpm php-cli php-common  

---

**5️⃣ Verify PHP Version**
php -v  

Expected:
PHP 8.2.x  

---

**6️⃣ Configure PHP-FPM**
sudo nano /etc/php-fpm.d/www.conf  

Update:

listen = /var/run/php-fpm/default.sock  
listen.owner = nginx  
listen.group = nginx  
listen.mode = 0660  

---

**7️⃣ Create Socket Directory**
sudo mkdir -p /var/run/php-fpm  

---

**8️⃣ Start Services**
sudo systemctl start php-fpm  
sudo systemctl enable php-fpm  

sudo systemctl start nginx  
sudo systemctl enable nginx  

---

▶️ **Verification**

From jump host:

Expected Output:
Welcome to xFusionCorp Industries!  


---

🧠 **How It Works**

- Nginx listens on port 8091  
- Requests for .php files are forwarded to PHP-FPM  
- PHP-FPM executes the PHP code  
- Communication happens via Unix socket  
- Output is returned to the client  


---

⚠️ **Common Mistakes**

- Installing wrong PHP version ❌  
- Not enabling PHP 8.2 module ❌  
- Incorrect socket path ❌  

- Missing PHP location block ❌  
- Not restarting services ❌  
- Wrong nginx port ❌  

---

💡 **Key Learnings**

- PHP-FPM executes PHP, Nginx serves requests  

- Unix sockets are faster than TCP for local communication  
- Version requirements matter in real-world setups  
- Proper configuration ensures seamless integration  

---

✅ **Final Status**

- Nginx installed and configured ✅  
- PHP-FPM 8.2 installed correctly ✅  
- Socket configured properly ✅  

- Nginx + PHP-FPM integration working ✅  
- PHP application accessible via curl ✅  
- Task completed successfully 🚀  

---
