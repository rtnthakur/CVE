# SQL Injection Vulnerability in Dairy Farm Shop Management System

## Overview
A SQL injection vulnerability was discovered in the PHPGurukul Dairy Farm Shop Management System (version 1.3). The vulnerability allows remote attackers to execute arbitrary SQL code via the `companyname` parameter in a POST request to `add-company.php`.

### Affected Product Details
- **Product Name**: Dairy Farm Shop Management System  
- **Vendor**: Phpgurukul  
- **Official Website**: [https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)  

| Affected Component      | Details                                                                 |
|-------------------------|-------------------------------------------------------------------------|
| Affected Code File      | `add-company.php`                                                      |
| Affected Parameter      | `companyname` (POST request)                                           |
| Vulnerability Type      | Time-based blind SQL injection                                         |
| Version Affected        | V1.3                                                                   |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.
    ![image](https://github.com/user-attachments/assets/76f3cd9a-fa7c-4bb3-80b7-12aa93040033)
 
2. **Navigate to the Company Section**  
   - Click the "Add Company" button.  
   - Enter any value in the input field.
    ![image](https://github.com/user-attachments/assets/f130aacd-983c-4e99-8bce-7a6b08820bdd)

3. **Intercept the Request**  
   - Use Burp Suite to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
    ![image](https://github.com/user-attachments/assets/cc0011c5-62e0-4154-b07f-b400f3019cef)

4. **Modify the Request**  
   - Capture the request when updating company details.  
   - Send it to Burp Suite Repeater.  
   - Inject the following payload into the `companyname` parameter:  
     ```sql
     '%2b(select*from(select(sleep(10)))a)%2b'
     ```
    ![image](https://github.com/user-attachments/assets/6b3b024b-b8cb-4fcd-8969-dd15103a269e)

5. **Confirm the Vulnerability**  
   - Forward the modified request.  
   - Observe a 10-second delay in the response, confirming the time-based SQL injection.
 -![image](https://github.com/user-attachments/assets/f88184bd-ed6c-4976-8f1c-41a0ac832ebf)

---

## Impact
- **Data Theft**: Unauthorized access to sensitive database information.  
- **Data Manipulation**: Alteration or deletion of critical data.  
- **Reconnaissance**: Enumeration of database structures for further attacks.  
- **Financial Loss**: Potential service disruption leading to monetary damages.  
- **Reputation Damage**: Loss of user trust due to security breaches.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize and validate all user inputs.  
2. **Prepared Statements**: Use parameterized queries to prevent SQL injection.  
3. **Output Encoding**: Encode data before rendering it in the application.  
4. **Content Security Policy (CSP)**: Implement CSP to mitigate HTML injection risks.  

For detailed guidance, refer to the [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  

---

 
