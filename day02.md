🟢 **Day 02: Temporary User Setup with Expiry ⏳👤**

---

📌 **Task Details (As Given)**  
As part of the temporary assignment to the Nautilus project, a developer named ravi requires access for a limited duration. To ensure smooth access management, a temporary user account with an expiry date is needed. Here's what you need to do:



Create a user named ravi on App Server 3 in Stratos Datacenter. Set the expiry date to 2027-04-15, ensuring the user is created in lowercase as per standard protocol.

Note: You can find the infrastructure details by clicking on the Details of all Users and Servers button on the top-right section of the page.

---

🤔 **What is Required?**  
- Create a new Linux user  
- Username: `ravi` (lowercase)  
- Set account expiry date  
- Execute on App Server 3 (`stapp03`)  

---

🔐 **Why This is Important?**  
- Prevents permanent access for temporary users  
- Enhances system security  
- Follows least privilege principle  
- Avoids stale/unused accounts  

---

🖥️ **Server Details**  
- Hostname: `stapp03`  
- User: `banner`  

---

⚙️ **Implementation Steps**

**1️⃣ Connect to Server**
```bash
ssh banner@stapp03
```
**2️⃣Create User with Expiry Date**
```bash
sudo useradd -m -e 2027-04-15 ravi
```

**3️⃣ Verify User Creation**
```bash
grep ravi /etc/passwd
```

**4️⃣ Verify Expiry Date**
```bash
sudo chage -l ravi
```

Expected Output:
```bash
Account expires : Apr 15, 2027
```

---

**▶️ Testing**

```bash
sudo chage -l ravi
```

✔ Before expiry → Login allowed
❌ After expiry → Login denied

---

**How It Works**

*useradd → Creates user
*-m → Creates home directory
*-e → Sets expiry date

After expiry:

*Account becomes inactive
*User cannot log in

---

**⚠️ Common Mistakes**

*Forgetting -e flag
*Wrong date format (YYYY-MM-DD)
*Not using sudo
*Not verifying with chage

---

**Final Status**

*User ravi created ✅
*Expiry set to 2027-04-15 ✅
*Verified successfully ✅
*Task completed 🎯

---
