# HTML Injection Vulnerability in Park Ticketing Management System (Search Function)

## Overview
An HTML Injection vulnerability was discovered in the `normal-search.php` file of the **PHPGurukul Park Ticketing Management System Project in PHP v2.0**. This vulnerability allows remote attackers to execute arbitrary code via the `searchdata` POST request parameter.

- **Official Website**: [Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)  
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL  

---

## Vulnerability Details
| **Field**           | **Details**                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Affected Vendor      | Phpgurukul                                                                  |
| Affected Code File   | `normal-search.php`                                                         |
| Affected Parameter   | `searchdata`                                                                |
| Method               | POST                                                                        |
| Type                 | HTML Injection                                                              |
| Version              | V2.0                                                                       |

---

## Steps to Reproduce
1. **Log in to the Admin Panel**  
   - Access the admin login page and enter valid credentials.  
   ![image](https://github.com/user-attachments/assets/f1d612a6-2536-4c20-8c74-240e48a38bb6)
  
2. **Navigate to PTMS Admin Section**  
   - Go to the "Search" section and select "Normal Ticket Search."  
   ![image](https://github.com/user-attachments/assets/948aec36-88d0-42b0-a619-8808d55a0695)

3. **Intercept the Request**  
   - Use Burp Suite to capture the request. Enable the interceptor to monitor traffic.  
   ![image](https://github.com/user-attachments/assets/da00d0d7-6d94-40f9-bea2-7bf5a6af7308)
  
4. **Modify the Request**  
   - Capture the request and send it to Burp Suite Repeater.  
   - Inject the payload into the `searchdata` parameter, e.g., `<h1>Hello</h1>`.  
   ![image](https://github.com/user-attachments/assets/36e3705f-8706-4b7f-b465-720fe7d02ddd)
  
5. **Observe the Result**  
   - The injected HTML is rendered on the page, confirming the vulnerability.  
   ![image](https://github.com/user-attachments/assets/70380f7b-74b1-4bd6-ac7f-005e2c45368e)

---

## Recommended Mitigations
- **Input Validation**: Sanitize and validate all user inputs to prevent malicious payloads.  
- **Output Encoding**: Encode output to neutralize injected HTML/JS code.  
- **Content Security Policy (CSP)**: Implement CSP headers to restrict unauthorized script execution.  
