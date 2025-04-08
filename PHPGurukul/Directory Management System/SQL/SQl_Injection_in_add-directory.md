# SQL Injection Vulnerability in PHPGurukul Directory Management System v2.0

## Overview
A SQL Injection vulnerability was discovered in the `/DMS/dms/admin/add-directory.php` file of the PHPGurukul Directory Management System Project in PHP v2.0. This vulnerability allows remote attackers to execute arbitrary code via the `fullname` parameter in a POST request.

- **Official Website**: [Directory Management System Using PHP and MySQL](https://phpgurukul.com/directory-management-system-using-php-and-mysql/)  
- **Affected Version**: v2.0  

### Vulnerability Details
| Affected Vendor       | Phpgurukul                     |
|-----------------------|--------------------------------|
| Affected Code File    | `add-directory.php`            |
| Affected Parameter    | `fullname`                     |
| Method                | POST                           |
| Type                  | Time-based blind SQL Injection |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Open the admin login page and enter valid credentials.  
   ![image](https://github.com/user-attachments/assets/5ccf27ca-d574-49ec-988e-a1729665f194)
  
2. **Navigate to Add Directory Section**  
   - Go to the "Directory" section and click "Add Directory."  
   ![image](https://github.com/user-attachments/assets/0c1545cb-9147-4c2f-b106-fc731f577c06)
  
3. **Enter Directory Details**  
   - Fill in fields like Full Name, Profession, Email, etc.  
   ![image](https://github.com/user-attachments/assets/2811b5fb-a9cc-4bc1-9ee7-54f243dabf3a)

4. **Intercept the Request**  
   - Use Burp Suite to intercept the request (proxy set to `127.0.0.1:8080`).  
   - Enable the Interceptor in the Proxy tab.  
   ![image](https://github.com/user-attachments/assets/ed782b43-63f6-4772-bc44-b69721b64545)
 
5. **Modify the Request**  
   - Capture the request and send it to Burp Suite Repeater.  
   - Inject the payload into the `fullname` parameter:  
     ```plaintext
     '+(select*from(select(sleep(20)))a)+'
     ```
   - ![image](https://github.com/user-attachments/assets/c5d41320-1a4a-4150-b4c9-fb5fdd3c5564)
  
6. **Confirm the Vulnerability**  
   - Forward the modified request and observe a 20-second delay in response, confirming the time-based SQL injection.  
   ![image](https://github.com/user-attachments/assets/bf864602-e40f-4eac-b383-2f6bc4ba11a1)

---

## Impact
- **Data Theft**: Unauthorized access to sensitive database data.  
- **Data Manipulation**: Alteration or deletion of data, compromising integrity.  
- **Reconnaissance**: Enumeration of database structures for further attacks.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize and validate all user inputs.  
2. **Prepared Statements**: Use parameterized queries to prevent SQL injection.  
3. **Content Security Policy (CSP)**: Implement CSP to mitigate HTML injection risks.  
4. **OWASP Guidelines**: Follow the [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  

--- 

**Note**: Immediate patching is advised to prevent exploitation.
