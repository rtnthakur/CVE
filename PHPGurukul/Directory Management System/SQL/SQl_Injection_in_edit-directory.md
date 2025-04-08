# SQL Injection Vulnerability in PHPGurukul Directory Management System v2.0 (edit-directory.php)

## Overview
A SQL Injection vulnerability was identified in the `/DMS/dms/admin/edit-directory.php` file of the PHPGurukul Directory Management System Project in PHP v2.0. Attackers can exploit this vulnerability via the `email` parameter in a POST request to execute arbitrary SQL commands.

- **Official Website**: [Directory Management System Using PHP and MySQL](https://phpgurukul.com/directory-management-system-using-php-and-mysql/)  
- **Affected Version**: v2.0  

### Vulnerability Details
| Affected Vendor       | Phpgurukul                     |
|-----------------------|--------------------------------|
| Affected Code File    | `edit-directory.php`           |
| Affected Parameter    | `email`                        |
| Method                | POST                           |
| Type                  | Time-based blind SQL Injection |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page and authenticate with valid credentials.  
   ![image](https://github.com/user-attachments/assets/ba13edbc-4e63-4b68-a642-5687d23a65ab)
  
2. **Navigate to Edit Directory Section**  
   - Go to "Directory by Status" > "Private" and click the **Edit** button for a record.  
   ![image](https://github.com/user-attachments/assets/a32c2447-2acd-4f07-8018-a7d63d60312e)
  
3. **Inject SQL Payload**  
   - In the editable `email` field, inject the payload:  
     ```plaintext
     '+(select*from(select(sleep(20)))a)+'
     ```
   - ![image](https://github.com/user-attachments/assets/d782aed7-a947-44e3-b4de-77f44fbb6d22)
  
4. **Intercept the Request**  
   - Use Burp Suite (proxy: `127.0.0.1:8080`) to intercept the request. Enable the **Interceptor** in the Proxy tab.  
   ![image](https://github.com/user-attachments/assets/94bd9af3-b804-436e-8627-34f96e610e24)
  
5. **Modify and Forward the Request**  
   - Capture the request, send it to Burp Repeater, and inject the payload.  
   ![image](https://github.com/user-attachments/assets/42141bc0-7afa-426e-9f22-c89af119ef98)

6. **Confirm the Vulnerability**  
   - Observe a 20-second delay in the server response, confirming time-based SQL injection.  
   ![image](https://github.com/user-attachments/assets/18078dbf-d284-402d-8243-a5734d180377)
  
---

## Impact
- **Data Theft**: Unauthorized extraction of sensitive database information.  
- **Data Tampering**: Malicious modification or deletion of records.  
- **Reconnaissance**: Mapping database structures for further attacks.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize user inputs (e.g., `email`) using allowlists or regex.  
2. **Prepared Statements**: Replace dynamic queries with parameterized queries.  
3. **Least Privilege**: Restrict database user permissions to minimize damage.  
4. **OWASP Guidelines**: Refer to the [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  

---

**Note**: Immediate remediation is critical to prevent exploitation of this vulnerability.
