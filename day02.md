# 🟢 Day 02: Temporary User Setup with Expiry ⏳👤

## 📌 Task Details
Create a user named `ravi` on **App Server 3** with an expiry date `2027-04-15`.

---

## 🤔 What is Required?
- Create a new Linux user
- Username: `ravi` (lowercase)
- Set account expiry date
- Execute on App Server 3 (`stapp03`)

---

## 🔐 Why This is Important?
- Prevents permanent access for temporary users
- Enhances system security
- Follows least privilege principle
- Avoids stale/unused accounts

---

## 🖥️ Server Details
- Hostname: `stapp03`
- User: `banner`

---

## ⚙️ Implementation Steps

### 1️⃣ Connect to Server
```bash
ssh banner@stapp03
```


