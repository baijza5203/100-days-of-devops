🟢 **Task Name**  
Day 01: Linux User Setup with Non-Interactive Shell 👤🚫

---

📌 **Task Details (As Given)**

To accommodate the backup agent tool's specifications, the system admin team at xFusionCorp Industries requires the creation of a user with a non-interactive shell.

Create a user named **anita** with a non-interactive shell on **App Server 2**.

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

---

🤔 **WHAT is being asked here?**

We need to:

* Create a **new Linux user**
* Name the user **anita**
* Assign a **non-interactive shell**
* Perform the task specifically on **App Server 2**

---

🤔 **WHY is this required?**

* Some users are created only for **services or automation tools**
* These users should **not have login access**
* Prevents:

  * Unauthorized access
  * Misuse of service accounts
* Improves **system security**

This is a **basic but critical system administration practice**.

---

⏰ **WHEN is this used in real life?**

* Backup agents
* Monitoring tools
* Application service accounts
* CI/CD pipelines
* System daemons

Example:  
A backup service may need a user account to access files but should **never allow human login**.

---

🧠 **HOW will the solution work? (High-level)**

1️⃣ Connect to App Server 2  
2️⃣ Create a user named `anita`  
3️⃣ Assign `/sbin/nologin` as the shell  
4️⃣ Verify user creation  

---

🖥️ **Infrastructure Context (Important)**

App Server 2

* Hostname: `stapp02`
* User: `steve`
* Purpose: Hosts Nautilus Application 2

---

⚠️ **Pre-Requisites (Must Be Done First)**

---

🔹 **Access the Server**

```bash
ssh steve@stapp02
🔹 Ensure sudo privileges


 **WHY:**

User creation requires administrative permissions.

⚙️ HOW the Solution Was Implemented

🔹 Step 1: Login to App Server 2

```bash
ssh steve@stapp02

🔹 Step 2: Create the user with non-interactive shell

```bash
sudo useradd -s /sbin/nologin anita

🔹 Alternative (if path differs)

```bash
sudo useradd -s /usr/sbin/nologin anita

🔹 Step 3: Verify user creation

```bash
grep anita /etc/passwd

Expected output:

anita:x:...:/sbin/nologin


  **▶️ HOW to Test the Configuration**

Try switching to the user:

```bash
su - anita

Expected result:

This account is currently not available.

This confirms non-interactive shell is working ✅

🧠** HOW the Solution Works**

useradd → Creates a new user
-s → Defines the login shell
/sbin/nologin → Prevents interactive login

When login is attempted:

System denies access
Displays a message instead of opening a shell

🚫 **WHY Non-Interactive Shell is Important**

Prevents direct login access
Secures service accounts
Reduces attack surface
Enforces least privilege principle

🧠** BEGINNER KEY TAKEAWAYS**

Not all users should have login access
/sbin/nologin is used to disable shell access
Service accounts are common in real systems
Always verify user configuration
Security starts with proper user management


  **⚠️ COMMON MISTAKES TO AVOID**

❌ Forgetting to specify shell
❌ Using /bin/bash instead of nologin
❌ Creating user on wrong server
❌ Not using sudo
❌ Not verifying the result

🎉 **FINAL STATUS**

✔ User anita created successfully
✔ Non-interactive shell assigned
✔ Login access restricted
✔ Verified configuration
✔ Task completed as per requirements
