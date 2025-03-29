# XSS Injection Vulnerability in Park Ticketing Management System

**Affected System:**  
Park Ticketing Management System Using PHP and MySQL (Version 2.0)  
**Vendor:** PHPGurukul  
**Official Website:** [https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)  

---

### Vulnerability Details

| **Field**               | **Details**                                                                 |
|-------------------------|-----------------------------------------------------------------------------|
| Affected Vendor         | PHPGurukul                                                                  |
| Affected Code File      | `normal-bwdates-reports-details.php`                                        |
| Vulnerable Parameters   | `fromdate`, `todate` (POST request)                                         |
| Attack Method           | POST                                                                        |
| Vulnerability Type      | Cross-Site Scripting (XSS)                                                  |
| Affected Version        | v2.0                                                                        |
| Impact                  | Remote arbitrary JavaScript execution via unsanitized user input.           |

---

### Steps to Reproduce
1. **Log in to the Admin Panel:**  
   - Access the admin login page and authenticate with valid credentials.
    ![image](https://github.com/user-attachments/assets/7ebe3020-13d0-4b95-b774-e10639569a68)
  
2. **Navigate to the Report Section:**  
   - Go to "Report" → "Normal People Report."  
   - Select any date range in the `fromdate` and `todate` fields.
    ![image](https://github.com/user-attachments/assets/de767dd7-f47b-4f85-96ce-c3b9ec0d22c7)
    
3. **Intercept the Request:**  
   - Use Burp Suite to capture the POST request.  
   - Enable the Interceptor to modify the request.
    ![image](https://github.com/user-attachments/assets/601f5dd3-a26a-412b-be11-4449d0eff685)

4. **Inject XSS Payload:**  
   - Modify the `fromdate` or `todate` parameter with:  
     ```html
     <script>alert(1)</script>
     ```
   - ![image](https://github.com/user-attachments/assets/d4d156bf-5375-4911-8cd6-48c47d1e8f75)

   - Forward the request.  

5. **Observe the Result:**  
   - The injected script executes, displaying an alert box.
   ![image](https://github.com/user-attachments/assets/a0c8856a-8729-496f-860b-e076a21cdb06)
  
---

### Recommended Mitigations
- Sanitize user inputs using functions like `htmlspecialchars()` or `strip_tags()`.  
- Implement Content Security Policy (CSP) headers.  
- Validate date formats strictly before processing.  
- Refer to:  
  - [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
  - [PortSwigger XSS Guide](https://portswigger.net/web-security/cross-site-scripting)  

---

**Note:** The vulnerability allows arbitrary code execution, posing a significant security risk. Immediate remediation is advised.  
