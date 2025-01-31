# 🚨 SQL Injection Vulnerability Report

## 🔍 Vulnerability Details

| Affected Product  | Beauty Parlour Management System |
|-------------------|---------------------------------|
| Affected Version | v1.1                            |
| Affected Vendor  | Open-source project            |
| Affected File    | `Beauty-Parlour-Management-System/bpms/index.php` |
| Affected Parameter | `name`                        |
| Request Method   | `POST`                          |
| Vulnerability Type | Time-based Blind SQL Injection |

---

## 🌐 Official Website
🔗 [Beauty Parlour Management System](https://repo.freeprojectscodes.com/?wpdmpro=download-beauty-parlor-management-system-source-code)

---

## ⚠️ Vulnerability Overview
This vulnerability allows remote attackers to exploit the `name` parameter in the Beauty Parlour Management System v1.1 by executing arbitrary SQL commands. Attackers can inject time-delay payloads to confirm SQL Injection flaws based on server response delays.

---

## 🛠️ Steps to Reproduce
### 1️⃣ Access the Target URL
```
http://localhost/Beauty-Parlour-Management-System/bpms/index.php
```
(Used for "Make an Appointment" feature.)
- ![image](https://github.com/user-attachments/assets/e757a0e8-d9d1-429c-a2cb-237a3529ea81)

### 2️⃣ Intercept the Request
- Configure Burp Suite and set up the browser to route traffic through it.
  ![image](https://github.com/user-attachments/assets/66c19d90-7157-440b-a278-17994237c9db)


### 3️⃣ Modify the Parameter
- Send the request to Burp Suite Repeater.
- Modify the `name` parameter with the following payload:
  ```
  ('%2b(select*from(select(sleep(20)))a)%2b')
  ```
  ![image](https://github.com/user-attachments/assets/4979bc12-9e0c-4390-8d3d-cd23dbe8b6a5)


### 4️⃣ Send the Modified Request
- Forward the request in Burp Suite Repeater.
- Observe the delay in response time.
- If the server delays its response by **20 seconds**, the SLEEP() function has been successfully executed, confirming a **time-based SQL injection vulnerability**.
  ![image](https://github.com/user-attachments/assets/7fc11fec-0dbd-49a4-8edd-eb3c65c9769c)

---

## 🔥 Impact of Exploitation
✅ **Data Theft:** Unauthorized access to sensitive user or system data.  
✅ **Data Manipulation:** Modification or deletion of critical data.  
✅ **Credential Exposure:** Potential leakage of usernames, passwords, or other authentication details.  
✅ **Server Compromise:** Exploiting database queries to attack the underlying server or gain shell access.  
✅ **Reconnaissance:** Enumeration of database structures (tables, columns, schemas) for further attacks.  
✅ **Financial Loss & Reputation Damage:** Service disruption leading to monetary losses and loss of user trust.

---

## 🛡️ Recommended Mitigations
🔹 **Use Parameterized Queries:** Ensure all SQL queries use prepared statements.  
🔹 **Implement Web Application Firewall (WAF):** To detect and block malicious requests.  
🔹 **Validate User Input:** Enforce strict input validation for all parameters.  
🔹 **Limit Database Privileges:** Restrict database user permissions to prevent unauthorized modifications.  
🔹 **Regular Security Audits:** Continuously monitor and test applications for SQL Injection vulnerabilities.  
🔹 **Follow Best Practices:** Refer to [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).

---

## 📌 Reported By
**Ratnesh Kumar**  
📩 Contact: [ratanthakur740@gmail.com](mailto:ratanthakur740@gmail.com)  

---
