
# HTML Injection Vulnerability in Park Ticketing Management System (Edit Ticket)

## Overview
An HTML Injection vulnerability was discovered in the `edit-ticket.php` file of the **Park Ticketing Management System Project in PHP v2.0** by PHPGurukul. This vulnerability allows remote attackers to execute arbitrary code via the `tickettype` and `tprice` POST request parameters.

- **Official Website**: [PHPGurukul Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL

---

## Vulnerability Details
| Affected Vendor       | PHPGurukul                          |
|-----------------------|-------------------------------------|
| Affected Code File    | `edit-ticket.php`                   |
| Affected Parameters   | `tickettype` and `tprice`           |
| Method                | POST                                |
| Type                  | HTML Injection                      |
| Version               | V2.0                                |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.  

2. **Navigate to the Manage Type Ticket Section**  
   - Go to the "Manage Type Ticket" section in the Admin Dashboard.  
   - Click the "Edit" button for any ticket.  

3. **Intercept the Request**  
   - Use **Burp Suite** to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.  

4. **Modify the Request**  
   - Capture the request when updating ticket details.  
   - Forward it to the Burp Suite Repeater.  
   - Inject the following payload into the `tickettype` or `tprice` parameter:  
     ```html
     <h1>Hello</h1>
     ```

5. **Send and Observe**  
   - The injected HTML will be rendered on the page, confirming the vulnerability.  

---

## Recommended Mitigations
- **Input Validation**: Implement strict input validation to filter malicious payloads.  
- **Output Encoding**: Encode output to prevent HTML/JavaScript execution.  
- **Content Security Policy (CSP)**: Deploy CSP headers to mitigate injection risks.  

---

**Security Note**: This vulnerability highlights the importance of implementing secure coding practices. Organizations should conduct regular security audits and penetration testing to identify and remediate such vulnerabilities before they can be exploited. Additionally, keeping all software components up-to-date is crucial for maintaining a secure environment.
