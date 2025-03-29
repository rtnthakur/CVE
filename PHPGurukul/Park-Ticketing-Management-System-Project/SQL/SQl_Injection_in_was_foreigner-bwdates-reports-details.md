# SQL Injection Vulnerability in Park Ticketing Management System

## Overview
A SQL Injection vulnerability was discovered in the `foreigner-bwdates-reports-details.php` file of the **Park Ticketing Management System Project in PHP v2.0** by PHPGurukul. This vulnerability allows remote attackers to execute arbitrary SQL code via the `todate` parameter in a POST request.

### Affected Product Details

| **Field**               | **Details**                                                                 |
|-------------------------|----------------------------------------------------------------------------|
| Product Name            | Park Ticketing Management System Using PHP and MySQL                       |
| Vendor                  | PHPGurukul                                                                 |
| Affected Code File      | `foreigner-bwdates-reports-details.php`                                    |
| Affected Parameter      | `todate`                                                                   |
| Method                  | POST                                                                       |
| Type                    | Time-based blind SQL Injection                                             |
| Version                 | v2.0                                                                       |
| Official Website        | [PHPGurukul PTMS](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/) |

---

## Steps to Reproduce
1. **Log in to the Admin Panel**  
   - Access the admin login page and enter valid credentials.
    ![image](https://github.com/user-attachments/assets/b77baff2-e2c6-4863-a666-22ff24031393)

2. **Navigate to the Report Section**  
   - Go to the "Report" section and select "Foreigners People Report."  
   - Choose any date range in the `fromdate` and `todate` input fields.
    ![image](https://github.com/user-attachments/assets/7fc987d3-a2f0-4316-bee9-342fd7008b23)

3. **Intercept the Request**  
   - Use Burp Suite to capture the request. Ensure the browser traffic is routed through Burp Suite.
    ![image](https://github.com/user-attachments/assets/67ecf545-1ff2-4414-97e4-af4309d870b5)
  
4. **Modify the Request**  
   - Capture the request and send it to Burp Suite Repeater.  
   - Inject the following payload into the `todate` parameter:  
     ```sql
     '%2b(select*from(select(sleep(20)))a)%2b'
     ```
   - ![image](https://github.com/user-attachments/assets/523bee1f-6012-4ceb-b241-59a85fa6dabf)

5. **Confirm the Vulnerability**  
   - Forward the modified request and observe a 20-second delay in the response, confirming the time-based SQL injection.
   ![image](https://github.com/user-attachments/assets/4a4a2ef3-268c-4a75-a73a-08bd6bc8f5ab)
  
---

## Impact
- **Data Theft**: Unauthorized access to sensitive database data.  
- **Data Manipulation**: Alteration or deletion of critical data.  
- **Reconnaissance**: Enumeration of database structures for further attacks.  
- **Financial Loss**: Potential service disruption leading to monetary losses.  
- **Reputation Damage**: Loss of user trust due to breaches or downtime.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize and validate all user inputs.  
2. **Prepared Statements**: Use parameterized queries to prevent SQL injection.  
3. **Output Encoding**: Encode data before rendering it in the application.  
4. **Content Security Policy (CSP)**: Implement CSP to mitigate HTML injection risks.  

For detailed guidance, refer to the [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  
