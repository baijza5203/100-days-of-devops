🟢 **Day 21: Create a Bare Git Repository on Storage Server 📦**

---

📌 **Task Details (As Given)**  
The Nautilus development team requested the DevOps team to set up a Git repository for a new application development project.

The task required installing Git on the Storage Server and creating a bare repository at a specific location.

---

🤔 **What is Required?**  
- Install Git using yum  
- Create a bare Git repository:
  /opt/apps.git  
- Ensure exact repository name is used  

---

🔐 **Why This is Important?**  
- Bare repositories are used as centralized remote repositories  
- Enables collaboration between developers  
- Essential for version control workflows  
- Commonly used in CI/CD and DevOps environments  

---

🖥️ **Server Details**

- Storage Server → ststor01 → User: natasha  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Storage Server**
ssh natasha@ststor01  

---

**2️⃣ Install Git**
sudo yum install -y git  

---

**3️⃣ Create Bare Repository**
sudo git init --bare /opt/apps.git  

---

▶️ **Verification**

Check repository:
ls -ld /opt/apps.git  

Verify bare repository:
git --git-dir=/opt/apps.git status  

Expected:
fatal: this operation must be run in a work tree  

(This confirms it is a bare repository.)  

---

🧠 **How It Works**

- Git manages version control for source code  
- A bare repository contains only Git metadata  
- No working directory exists in a bare repo  
- Used as a shared remote repository for teams  

---

⚠️ **Common Mistakes**

- Forgetting --bare option ❌  
- Creating repository with wrong name ❌  
- Creating repository in wrong path ❌  
- Not installing Git before initialization ❌  

---

💡 **Key Learnings**

- Bare repositories are different from normal repositories  
- Bare repos are mainly used as remote/shared repos  
- Git can be initialized directly in a target path  
- Proper naming and path matter in automation tasks  

---

✅ **Final Status**

- Git installed successfully ✅  
- Bare repository created successfully ✅  
- Repository path verified ✅  
- Task completed successfully 🚀  

---
