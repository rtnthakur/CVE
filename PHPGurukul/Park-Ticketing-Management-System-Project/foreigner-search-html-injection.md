# HTML Injection Vulnerability in Park Ticketing Management System (Foreigner Search)

## Overview
An HTML Injection vulnerability was discovered in the `foreigner-search.php` file of the **Park Ticketing Management System Project in PHP v2.0** by PHPGurukul. This vulnerability allows remote attackers to execute arbitrary code via the `searchdata` POST request parameter.

- **Official Website**: [PHPGurukul Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL

---

## Vulnerability Details

| Category              | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| Vendor                | PHPGurukul                                                             |
| Affected Component    | `foreigner-search.php`                                                 |
| Vulnerable Parameter  | `searchdata`                                                           |
| Attack Vector         | POST Request                                                           |
| Vulnerability Type    | HTML Injection                                                         |
| Impact                | Cross-Site Scripting (XSS), Session Hijacking, UI Spoofing             |
| Affected Version      | v2.0                                                                   |
| CWE ID                | CWE-79: Improper Neutralization of Input During Web Page Generation    |
| CVSS Score            | 6.1 (Medium)                                                           |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.
    ![image](https://github.com/user-attachments/assets/cbe1adc5-2d9e-43f5-ae22-d8708c81d4ba)

2. **Navigate to the Search Section**  
   - Go to the "Search" section in the Admin Dashboard.  
   - Click on "Foreigners Ticket Search".
    ![image](https://github.com/user-attachments/assets/1cb7b6b8-f872-4730-a5aa-48a407479310)
 
3. **Intercept the Request**  
   - Use **Burp Suite** to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
    ![image](https://github.com/user-attachments/assets/de3d4b6a-a92f-495b-945b-0aef8b7cb31c)
 
4. **Modify the Request**  
   - Capture the request when performing a search.  
   - Forward it to the Burp Suite Repeater.  
   - Inject the following payload into the `searchdata` parameter:  
     ```html
     <h1>Hello</h1>
     ```
   - ![image](https://github.com/user-attachments/assets/b8a91c7f-edd4-4ce7-9cf2-4d81ccd4e3f5)

5. **Send and Observe**  
   - The injected HTML will be rendered on the page to confirm the vulnerability.
   ![image](https://github.com/user-attachments/assets/b5266d8b-8d16-4d54-90d7-a3bf23dc536e)
  

---

## Recommended Mitigations
- **Input Validation**: Implement strict input validation to filter malicious payloads.  
- **Output Encoding**: Encode output to prevent HTML/JavaScript execution.  
- **Content Security Policy (CSP)**: Deploy CSP headers to mitigate injection risks.  

---

**Security Note**: This high-severity vulnerability (CVSS 7.3) could allow attackers to manipulate search results and potentially compromise user sessions. Immediate remediation is required, including implementing the suggested security measures and conducting a comprehensive security review of all input handling mechanisms in the application.
