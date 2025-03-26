# HTML Injection Vulnerability in Park Ticketing Management System

## Overview
An HTML Injection vulnerability was discovered in the `normal-bwdates-reports-details.php` file of the **PHPGurukul Park Ticketing Management System Project in PHP v2.0**. This vulnerability allows remote attackers to execute arbitrary code via the `fromdate` and `todate` POST request parameters.

- **Official Website**: [Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)  
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL  

---

## Vulnerability Details
| **Field**           | **Details**                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Affected Vendor      | Phpgurukul                                                                  |
| Affected Code File   | `normal-bwdates-reports-details.php`                                        |
| Affected Parameters  | `fromdate` and `todate`                                                     |
| Method               | POST                                                                        |
| Type                 | HTML Injection                                                              |
| Version              | V2.0                                                                       |

---

## Steps to Reproduce
1. **Log in to the Admin Panel**  
   - Access the admin login page and enter valid credentials.  
   ![image](https://github.com/user-attachments/assets/97db1532-70a6-49a2-9d30-678374a25cad)
  
2. **Navigate to PTMS Admin Section**  
   - Go to the "Report" section and select "Normal People Report."  
   ![image](https://github.com/user-attachments/assets/37433f5e-46d6-4242-be2d-75c0c93a2223)
  
3. **Intercept the Request**  
   - Use Burp Suite to capture the request. Enable the interceptor to monitor traffic.  
   ![image](https://github.com/user-attachments/assets/e2160783-0c0b-464b-b147-c9cb57e47296)

4. **Modify the Request**  
   - Capture the request and send it to Burp Suite Repeater.  
   - Inject the payload into the `fromdate` or `todate` parameters, e.g., `<h1>Hello</h1>`.  
   ![image](https://github.com/user-attachments/assets/122040ab-e696-4579-98bf-aa9af8322629)
  
5. **Observe the Result**  
   - The injected HTML is rendered on the page, confirming the vulnerability.  
   ![image](https://github.com/user-attachments/assets/45ee8da5-2169-4b9b-9ad0-c5b83f7a7224)

---

## Recommended Mitigations
- **Input Validation**: Sanitize and validate all user inputs to prevent malicious payloads.  
- **Output Encoding**: Encode output to neutralize injected HTML/JS code.  
- **Content Security Policy (CSP)**: Implement CSP headers to restrict unauthorized script execution.  
