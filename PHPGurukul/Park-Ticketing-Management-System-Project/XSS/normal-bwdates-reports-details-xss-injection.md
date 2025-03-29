# Cross-Site Scripting (XSS) Vulnerability in Park Ticketing Management System (Normal Reports)

**Vendor**: PHPGurukul  
**Affected Product**: Park Ticketing Management System Using PHP and MySQL  
**Affected Version**: v2.0  
**Vulnerability Type**: XSS Injection  
**Affected File**: `ptms/normal-bwdates-reports-details.php`  
**Affected Parameters**: `fromdate` and `todate` (POST request)  
**Official Website**: [https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)  

---

## **Description**
A Cross-Site Scripting (XSS) vulnerability was identified in the `normal-bwdates-reports-details.php` file of the PHPGurukul Park Ticketing Management System. Attackers can inject malicious JavaScript code via the `fromdate` and `todate` parameters in POST requests, leading to arbitrary script execution in the victim's browser context.

---

## **Steps to Reproduce**
1. **Log in to the Admin Panel**  
   - Access the admin login page and authenticate with valid credentials.
   ![image](https://github.com/user-attachments/assets/ead81c5f-6eff-4848-96af-8a74f99b7d32)
  
2. **Navigate to the Report Section**  
   - Go to the "Report" section and select "Normal People Report."
   ![image](https://github.com/user-attachments/assets/3f99f1d7-ee8c-48bf-94ad-cc8cfb9704ea)
  
3. **Intercept the Request**  
   - Use Burp Suite to intercept the POST request containing the `fromdate` and `todate` parameters.
   ![image](https://github.com/user-attachments/assets/3d5e44cc-8acf-431a-92f7-38b3069a7492)
  
4. **Inject XSS Payload**  
   - Modify the parameters with the following payloads:  
     - `fromdate`: `<script>alert(1)</script>`  
     - `todate`: `<script>alert(2)</script>`
   - ![image](https://github.com/user-attachments/assets/ed3052f0-405a-4bca-8309-4ace04c2e661)
 
5. **Observe the Result**  
   - The injected script executes upon rendering the manipulated input.
   ![image](https://github.com/user-attachments/assets/25b51af2-e343-4e19-a2b3-aa45697eee91)
   ![image](https://github.com/user-attachments/assets/f7070698-4378-4497-8619-d242b811952a)


## **Mitigation Recommendations**
- **Input Validation**: Sanitize and validate all user-supplied data.  
- **Output Encoding**: Encode dynamic content before rendering (e.g., HTML entities).  
- **Security Libraries**: Use tools like HTMLPurifier for robust sanitization.  
- **OWASP Guidelines**: Follow best practices from:  
  - [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
- **Developer Training**: Educate teams on secure coding practices.  

---

## **References**
- [PHPGurukul Official Website](https://phpgurukul.com/)  
- [PortSwigger XSS Guide](https://portswigger.net/web-security/cross-site-scripting)  
- [OWASP XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
