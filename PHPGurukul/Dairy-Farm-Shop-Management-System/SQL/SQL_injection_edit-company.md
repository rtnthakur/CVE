# SQL Injection Vulnerability in Dairy Farm Shop Management System (Company Module)

## Overview
A time-based blind SQL injection vulnerability was identified in the PHPGurukul Dairy Farm Shop Management System (Version 1.3). The vulnerability exists in the `manage-companies.php` file and allows remote attackers to execute arbitrary SQL code via the `companyname` parameter in a POST request.

**Official Website**: [Dairy Farm Shop Management System](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)

---

## Vulnerability Details
| **Field**           | **Details**                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Affected Vendor     | Phpgurukul                                                                 |
| Affected Code File  | `manage-companies.php`                                                     |
| Affected Parameter  | `companyname`                                                              |
| Method              | POST                                                                       |
| Type                | Time-based blind SQL injection                                            |
| Version             | V1.3                                                                      |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**
   - Access the admin login page.
   - Authenticate with valid credentials.
    ![image](https://github.com/user-attachments/assets/7ccc03b0-47ad-4d35-be5c-38bbfe706ede)

2. **Navigate to the Company Section**
   - Click the "manage" button for company management.
   - Select the "edit" (pencil icon) option for a company.
    ![image](https://github.com/user-attachments/assets/ac5f9e58-8b63-4b73-9a8f-0f46c566ee91)
   - Click the "update" button without modifying any fields.
    ![image](https://github.com/user-attachments/assets/6b27d359-b2be-45c3-9062-8a4ac2d0f6b9)

3. **Intercept the Request**
   - Use Burp Suite to intercept the HTTP traffic.
   - Capture the POST request during the update action.
    ![image](https://github.com/user-attachments/assets/e364ec55-8274-4c87-9bcd-1f64edaaac68)

4. **Modify the Request**
   - Forward the captured request to Burp Suite Repeater.
   - Inject the payload into the `companyname` parameter:  
     `'%2b(select*from(select(sleep(20)))a)%2b'`
    ![image](https://github.com/user-attachments/assets/2ecfdd13-683e-455c-941c-3d0b0654bc8c)

5. **Confirm the Vulnerability**
   - Observe a 20-second delay in the server response.
   - This confirms successful execution of the `SLEEP()` function, proving the SQL injection flaw.
    ![image](https://github.com/user-attachments/assets/8d4e61ca-385a-416b-a481-d2544070f4e0)

---

## Impact
- **Data Theft**: Unauthorized extraction of sensitive database information.
- **Data Manipulation**: Alteration or deletion of critical company records.
- **System Reconnaissance**: Mapping of database schema for further attacks.
- **Operational Disruption**: Potential denial of service affecting business operations.
- **Reputational Harm**: Loss of customer trust due to compromised data security.

---

## Recommended Mitigations
- **Input Validation**: Sanitize all user-supplied input for the `companyname` parameter.
- **Prepared Statements**: Use parameterized queries to separate SQL logic from data.
- **Database Permissions**: Restrict database user privileges to minimum required.
- **Web Application Firewall**: Deploy a WAF to filter malicious SQL payloads.
- **Security Headers**: Implement CSP headers to reduce injection risks.

**Reference**: [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

---

