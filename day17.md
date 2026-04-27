🟢 **Day 17: Configure PostgreSQL Database and User 🐘**

---

📌 **Task Details (As Given)**  
The Nautilus application development team plans to deploy a new application that uses a PostgreSQL database. As a prerequisite, the PostgreSQL database server must be configured with a specific user and database.

PostgreSQL is already installed on the database server.

---

🤔 **What is Required?**  
- Create a PostgreSQL user: kodekloud_sam  
- Set password: YchZHRcLkL  
- Create database: kodekloud_db7  
- Grant full permissions to the user on this database  
- Do NOT restart PostgreSQL service  

---

🔐 **Why This is Important?**  
- Enables secure database authentication  
- Prepares backend for application deployment  
- Demonstrates user and privilege management in PostgreSQL  
- Ensures no service disruption  

---

🖥️ **Server Details**

- Database Server → stdb01 → User: peter  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Database Server**
ssh peter@stdb01  

---

**2️⃣ Switch to PostgreSQL User**
sudo su - postgres  

---

**3️⃣ Access PostgreSQL Shell**
psql  

---

**4️⃣ Create Database User**
CREATE USER kodekloud_sam WITH PASSWORD 'YchZHRcLkL';  

---

**5️⃣ Create Database**
CREATE DATABASE kodekloud_db7;  

---

**6️⃣ Grant Privileges**
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db7 TO kodekloud_sam;  

---

**7️⃣ Exit PostgreSQL**
\q  
exit  

---

▶️ **Verification**
psql -U kodekloud_sam -d kodekloud_db7 -h localhost  

Expected:
Successful login and prompt like:
kodekloud_db7=>  

---

🧠 **How It Works**

- PostgreSQL uses roles to manage users  
- A database is created for application data  
- Permissions allow the user full control over the database  
- Changes apply instantly without restarting the service  

---

⚠️ **Common Mistakes**

- Forgetting quotes around password ❌  
- Not switching to postgres user ❌  
- Missing GRANT statement ❌  
- Typo in username or database name ❌  
- Attempting to restart PostgreSQL ❌  

---

💡 **Key Learnings**

- PostgreSQL user = role  
- Permissions must be explicitly granted  
- No restart required after changes  
- Always verify by logging in with new credentials  

---

✅ **Final Status**
- User created successfully ✅  
- Database created successfully ✅  
- Permissions granted correctly ✅  
- Login verified successfully ✅  
- Task completed 🚀  
---

