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
| Affected Code File      | `foreigner-bwdates-reports-details.php`                                     |
| Vulnerable Parameters   | `fromdate`, `todate` (POST request)                                        |
| Attack Method           | POST                                                                        |
| Vulnerability Type      | Cross-Site Scripting (XSS)                                                 |
| Affected Version        | v2.0                                                                        |
| Impact                  | Remote arbitrary JavaScript execution via unsanitized user input.           |

---

### Steps to Reproduce
1. **Log in to the Admin Panel:**  
   - Access the admin login page and authenticate with valid credentials.
    ![image](https://github.com/user-attachments/assets/e570247e-32f3-41f6-8737-14e2072fc0fa)

2. **Navigate to the Report Section:**  
   - Go to "Report" → "Foreigners People Report."  
   - Select any date range in the `fromdate` and `todate` fields.
    ![image](https://github.com/user-attachments/assets/49be39be-d969-4bf2-a084-2d6b095d0f36)
  
3. **Intercept the Request:**  
   - Use Burp Suite to capture the POST request.  
   - Enable the Interceptor to modify the request.
    ![image](https://github.com/user-attachments/assets/86cd0e80-b19f-4dcc-965e-a9c7475bce30)
  
4. **Inject XSS Payload:**  
   - Modify the `fromdate` or `todate` parameter with:  
     ```html
     <script>alert(1)</script>
     ```
   - ![image](https://github.com/user-attachments/assets/cb112a7c-1772-4300-84cf-05a55fd40f93)
   
   - Forward the request.  

6. **Observe the Result:**  
   - The injected script executes, displaying an alert box.
   ![image](https://github.com/user-attachments/assets/442da82a-086c-4df1-b9d8-3c93587a3b0c)
  

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
