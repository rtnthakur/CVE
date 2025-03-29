# SQL Injection Vulnerability in Park Ticketing Management System (Edit Ticket)

## Overview
A SQL injection vulnerability was discovered in the "Park-Ticketing-Management-System-Project/ptms/edit-ticket.php" file of the PHPGurukul Park Ticketing Management System Project in PHP v2.0. This vulnerability allows remote attackers to execute arbitrary code via the `tprice` POST request parameter.

### Official Website
- **URL:** [https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)

### Affected Product
| **Field**          | **Details**                                  |
|--------------------|---------------------------------------------|
| Vendor             | Phpgurukul                                  |
| Product Name       | Park Ticketing Management System Using PHP and MySQL |
| Version            | V2.0                                        |
| Affected Code File | `edit-ticket.php`                           |
| Affected Parameter | `tprice`                                    |
| Method             | POST                                        |
| Vulnerability Type | Time-based blind                            |

---

## Steps to Reproduce

1. **Log in to the Admin Panel:**
   - Open the admin login page.
   - Enter credentials and sign in.  
   ![Login Page](media/image1.png)

2. **Navigate to Admin Dashboard:**
   - Go to the "Manage Type Ticket" section.
   - Click the "Edit" button.  
   ![Manage Type Ticket Section](media/image2.png)
   - Make changes to the ticket and click "Update".  
   ![Update Ticket](media/image3.png)

3. **Intercept the Request:**
   - Use Burp Suite to capture traffic.
   - Enable the interceptor to capture the request.  
   ![Burp Suite Interceptor](media/image4.png)

4. **Modify the Request:**
   - Capture the request when updating ticket details.
   - Send it to Burp Suite Repeater.
   - Inject the payload into the `tprice` parameter:  
     ```
     (('%2b(select*from(select(sleep(20)))a)%2b'))
     ```  
   ![Payload Injection](media/image5.png)

5. **Send the Modified Request:**
   - Forward the request in Burp Suite Repeater.
   - Observe a 20-second delay in response, confirming the SQL injection.  
   ![Delayed Response](media/image6.png)

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
