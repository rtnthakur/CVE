# HTML Injection Vulnerability in Park Ticketing Management System

## Overview
An HTML Injection vulnerability was discovered in the `add-foreigners-ticket.php` file of the **Park Ticketing Management System Project in PHP v2.0** by PHPGurukul. This vulnerability allows remote attackers to execute arbitrary code via the `cprice` POST request parameter.

- **Official Website**: [PHPGurukul Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL

---

## Vulnerability Details
| Affected Vendor       | PHPGurukul                          |
|-----------------------|-------------------------------------|
| Affected Code File    | `add-foreigners-ticket.php`         |
| Affected Parameter    | `cprice`                            |
| Method                | POST                                |
| Type                  | HTML Injection                      |
| Version               | V2.0                                |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.
   ![image](https://github.com/user-attachments/assets/c6dec6cc-3bb5-4e8f-83a4-d242ea01ad55)

2. **Navigate to the Foreigners Ticket Section**  
   - Go to the "Foreigners Ticket" section.  
   - Click the "Add Ticket" button and fill in the input fields.
   ![image](https://github.com/user-attachments/assets/a2a735a1-d47f-487d-a632-c53bd99cd3f3)

3. **Intercept the Request**  
   - Use **Burp Suite** to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
   ![image](https://github.com/user-attachments/assets/131074b7-e4d0-46d8-86ed-46af8e38cef6)
 
4. **Modify the Request**  
   - Capture the request when updating user details.  
   - Forward it to the Burp Suite Repeater.  
   - Inject the following payload into the `cprice` parameter:  
     ```html
     <h1>Hello</h1>
     ```
   - ![image](https://github.com/user-attachments/assets/e812015d-18c5-44c1-9c3e-35c7f97604ee)
   
5. **Send and Observe**  
   - The injected HTML will be rendered on the page to confirm the vulnerability.
   ![image](https://github.com/user-attachments/assets/32a7fec4-4b2d-4032-a296-5415c9e66630)
 

---

## Recommended Mitigations
- **Input Validation**: Implement strict input validation to filter malicious payloads.  
- **Output Encoding**: Encode output to prevent HTML/JavaScript execution.  
- **Content Security Policy (CSP)**: Deploy CSP headers to mitigate injection risks.  

---

**Note**: Always update systems and follow secure coding practices to prevent such vulnerabilities.
