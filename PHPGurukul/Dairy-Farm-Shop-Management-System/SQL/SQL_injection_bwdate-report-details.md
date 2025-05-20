# SQL Injection Vulnerability in Dairy Farm Shop Management System (Date Range Report)

## Overview
A SQL injection vulnerability was discovered in the PHPGurukul Dairy Farm Shop Management System (version 1.3). The vulnerability allows remote attackers to execute arbitrary SQL code via the `fromdate` and `todate` parameters in a POST request to `bwdate-report-ds.php`.

### Affected Product Details
- **Product Name**: Dairy Farm Shop Management System  
- **Vendor**: Phpgurukul  
- **Official Website**: [https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)  

| Affected Component      | Details                                                                 |
|-------------------------|-------------------------------------------------------------------------|
| Affected Code File      | `bwdate-report-ds.php`                                                 |
| Affected Parameters     | `fromdate`, `todate` (POST request)                                    |
| Vulnerability Type      | Time-based blind SQL injection                                         |
| Version Affected        | V1.3                                                                   |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.
    ![image](https://github.com/user-attachments/assets/37ffcbc5-7bc4-4140-a701-996eaaaea25e)
  
2. **Navigate to the Reports Section**  
   - Click the "B/w Dates" button to select a date range.  
   - Choose dates in the input fields.
   ![image](https://github.com/user-attachments/assets/906405cf-fdd9-4fc8-91a9-5f25e58ba84d)
   
3. **Intercept the Request**  
   - Use Burp Suite to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
    ![image](https://github.com/user-attachments/assets/8614afd1-e4f1-47c1-bf45-cbed03cb6987)

4. **Modify the Request**  
   - Capture the request when submitting date range details.  
   - Send it to Burp Suite Repeater.  
   - Inject the following payload into either the `fromdate` or `todate` parameter:  
     ```sql
     '%2b(select*from(select(sleep(20)))a)%2b'
     ```
  - ![image](https://github.com/user-attachments/assets/60ffd7a8-f6bd-4eb7-b916-719fcdcdee17)

5. **Confirm the Vulnerability**  
   - Forward the modified request.  
   - Observe a 15-second delay in the response, confirming the time-based SQL injection.
   ![image](https://github.com/user-attachments/assets/8501e2d8-d6df-462f-a03a-232193cc904d)
  

---

## Impact
- **Data Theft**: Unauthorized access to sensitive database information.  
- **Data Manipulation**: Alteration or deletion of critical data.  
- **Reconnaissance**: Enumeration of database structures for further attacks.  
- **Financial Loss**: Potential service disruption leading to monetary damages.  
- **Reputation Damage**: Loss of user trust due to security breaches.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize and validate all user inputs, especially date fields.  
2. **Prepared Statements**: Use parameterized queries to prevent SQL injection.  
3. **Output Encoding**: Encode data before rendering it in the application.  
4. **Content Security Policy (CSP)**: Implement CSP to mitigate HTML injection risks.  

For detailed guidance, refer to the [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  

--- 
