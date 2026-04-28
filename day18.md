🟢 **Day 18: Install and Configure DB Server**

---

📌 **Task Details (As Given)**  
We need to set up a MariaDB database server on the Nautilus DB Server in Stratos Datacenter. The task involves installing MariaDB, creating a database, creating a user, and granting appropriate permissions.

---

🤔 **What is Required?**  
- Install and configure MariaDB server  
- Create database: kodekloud_db7  
- Create user: kodekloud_sam  
- Set password: B4zNgHA7Ya  
- Grant full permissions to the user on the database  

---

🔐 **Why This is Important?**  
- Enables structured data storage for applications  
- Ensures secure access through user authentication  
- Demonstrates database setup and privilege management  
- Prepares system for production-level deployments  

---

🖥️ **Server Details**

- Database Server → stdb01 → User: peter  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Database Server**
ssh peter@stdb01  

---

**2️⃣ Install MariaDB**
sudo yum install -y mariadb-server  

---

**3️⃣ Start and Enable MariaDB**
sudo systemctl start mariadb  
sudo systemctl enable mariadb  

---

**4️⃣ Access MariaDB Shell**
sudo mysql  

---

**5️⃣ Create Database**
CREATE DATABASE kodekloud_db7;  

---

**6️⃣ Create User**
CREATE USER 'kodekloud_sam'@'localhost' IDENTIFIED BY 'B4zNgHA7Ya';  

---

**7️⃣ Grant Permissions**
GRANT ALL PRIVILEGES ON kodekloud_db7.* TO 'kodekloud_sam'@'localhost';  

---

**8️⃣ Apply Changes**
FLUSH PRIVILEGES;  

---

**9️⃣ Exit**
EXIT;  

---

▶️ **Verification**

Login using new user:
mysql -u kodekloud_sam -p  

Enter password:
B4zNgHA7Ya  

Then run:
USE kodekloud_db7;  

Expected:
Database selected successfully without errors  

---

🧠 **How It Works**

- MariaDB manages databases and users  
- A database is created for application data  
- A user is created with authentication credentials  
- Permissions allow full access to the database  
- FLUSH PRIVILEGES ensures changes are applied immediately  

---

⚠️ **Common Mistakes**

- Forgetting FLUSH PRIVILEGES ❌  
- Typo in username or password ❌  
- Not starting MariaDB service ❌  
- Missing 'localhost' in user creation ❌  
- Incorrect database name in GRANT command ❌  

---

💡 **Key Learnings**

- Database and user setup are core DevOps skills  
- Permissions must be explicitly granted  
- Services must be running before configuration  
- Always verify by logging in with created user  

---

✅ **Final Status**

- MariaDB installed and running ✅  
- Database created successfully ✅  
- User created successfully ✅  
- Permissions granted correctly ✅  
- Login verified successfully ✅  
- Task completed 🚀  

---
