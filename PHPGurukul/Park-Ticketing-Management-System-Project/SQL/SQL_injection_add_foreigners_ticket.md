# SQL Injection Vulnerability in Park Ticketing Management System

## Overview
A SQL injection vulnerability was discovered in the "Park-Ticketing-Management-System-Project/ptms/add-foreigners-ticket.php" file of the PHPGurukul Park Ticketing Management System Project in PHP v2.0. This vulnerability allows remote attackers to execute arbitrary code via the `cprice` POST request parameter.

### Official Website
- **URL:** [https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)

### Affected Product
- **Name:** Park Ticketing Management System Using PHP and MySQL  
- **Vendor:** Phpgurukul  
- **Version:** V2.0  

### Vulnerability Details
| **Field**           | **Details**                                  |
|---------------------|---------------------------------------------|
| Affected Code File  | `add-foreigners-ticket.php`                 |
| Affected Parameter  | `cprice`                                    |
| Method              | POST                                        |
| Type                | Time-based blind                            |

---

## Steps to Reproduce

1. **Log in to the Admin Panel:**
   - Open the admin login page.
   - Enter credentials and sign in.  
   ![image](https://github.com/user-attachments/assets/8f690ce0-6d84-4847-bd13-9ce45cf2f1e6)

2. **Navigate to Profile Section:**
   - Go to the "Foreigners Ticket" section.
   - Click "Add Ticket" and fill in the input fields.  
   ![image](https://github.com/user-attachments/assets/ac627118-57e5-4bcb-9999-4aa0b3e45d16)

3. **Intercept the Request:**
   - Use Burp Suite to capture traffic.
   - Enable the interceptor to capture the request.  
   ![image](https://github.com/user-attachments/assets/14dff3fd-87d4-4f0f-ab98-80d2fa8ff8a2)

4. **Modify the Request:**
   - Capture the request when updating user details.
   - Send it to Burp Suite Repeater.
   - Inject the payload into the `cprice` parameter:  
     ```
     (('%2b(select*from(select(sleep(20)))a)%2b'))
     ```  
   - ![image](https://github.com/user-attachments/assets/55e40b00-2b45-457c-991f-8e0128feb020)

5. **Send the Modified Request:**
   - Forward the request in Burp Suite Repeater.
   - Observe a 20-second delay in response, confirming the SQL injection.  
   ![image](https://github.com/user-attachments/assets/a2b6d870-650c-4e91-b5e4-95fc52a4d543)

---

## Impact
- **Data Theft:** Unauthorized access to sensitive data.  
- **Data Manipulation:** Alteration or deletion of database records.  
- **Reconnaissance:** Enumeration of database structure for further attacks.  
- **Financial Loss:** Service disruption leading to monetary losses.  
- **Reputation Damage:** Loss of user trust due to breaches or downtime.  

---

## Recommended Mitigations
1. **Input Validation:** Sanitize and validate all user inputs.  
2. **Output Encoding:** Encode outputs to prevent malicious execution.  
3. **Content Security Policy (CSP):** Implement CSP to mitigate injection risks.  
4. **Use Prepared Statements:** Parameterized queries to prevent SQL injection.  

### Resources
- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
