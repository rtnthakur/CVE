# SQL Injection Vulnerability in Dairy Farm Shop Management System (Login Page)

## Overview
A critical time-based blind SQL injection vulnerability was discovered in the login page (`index.php`) of PHPGurukul's Dairy Farm Shop Management System (Version 1.3). Attackers can exploit the `username` parameter in POST requests to execute arbitrary SQL commands, potentially compromising the entire system.

**Official Website**: [Dairy Farm Shop Management System](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)

---

## Vulnerability Details
| **Field**           | **Details**                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Affected Vendor     | Phpgurukul                                                                 |
| Affected Code File  | `index.php`                                                                |
| Affected Parameter  | `username`                                                                 |
| Method              | POST                                                                       |
| Type                | Time-based blind SQL injection                                            |
| Version             | V1.3                                                                      |

---

## Steps to Reproduce

1. **Access the Login Page**
   - Navigate to the system's login interface.
    ![image](https://github.com/user-attachments/assets/e3e182be-30d5-4151-a554-1e1227122a1f)

2. **Intercept Login Request**
   - Configure Burp Suite to intercept traffic
   - Attempt login with any credentials (valid or invalid)
   - Capture the POST request containing the `username` parameter
    ![image](https://github.com/user-attachments/assets/7bc0ea7c-0dc0-4610-bfdc-5f1b2e788aac)

3. **Inject Malicious Payload**
   - Send intercepted request to Burp Repeater
   - Modify `username` parameter with:  
     `'%2b(select*from(select(sleep(20)))a)%2b'`
    ![image](https://github.com/user-attachments/assets/affb458c-990a-49ac-88ef-776b27aa10bb)

4. **Verify Exploitation**
   - Observe 20-second response delay
   - This confirms successful SQL command execution via time-based injection.
   ![image](https://github.com/user-attachments/assets/0e983a74-091c-41cd-bb23-bc10c584a2bd)

---

## Impact
- **Complete System Compromise**: Attackers can bypass authentication
- **Database Exfiltration**: Extraction of admin credentials and sensitive data
- **Persistent Backdoors**: Potential creation of admin accounts
- **Business Disruption**: Denial of service through database locks
- **Regulatory Consequences**: Violations of data protection laws (GDPR, etc.)

---

## Recommended Mitigations
- **Input Validation**: Sanitize all user-supplied input for the `companyname` parameter.
- **Prepared Statements**: Use parameterized queries to separate SQL logic from data.
- **Database Permissions**: Restrict database user privileges to minimum required.
- **Web Application Firewall**: Deploy a WAF to filter malicious SQL payloads.
- **Security Headers**: Implement CSP headers to reduce injection risks.

**Reference**: [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

---

