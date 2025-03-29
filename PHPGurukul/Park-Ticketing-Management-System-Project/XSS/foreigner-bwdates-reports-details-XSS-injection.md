# Cross-Site Scripting (XSS) Vulnerability in Park Ticketing Management System

**Vendor**: PHPGurukul  
**Affected Product**: Park Ticketing Management System Using PHP and MySQL  
**Affected Version**: v2.0  
**Vulnerability Type**: XSS Injection  
**Affected File**: `ptms/foreigner-bwdates-reports-details.php`  
**Affected Parameters**: `fromdate` and `todate` (POST request)  
**Official Website**: [https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)  

---

## **Description**
A Cross-Site Scripting (XSS) vulnerability was discovered in the `foreigner-bwdates-reports-details.php` file of the PHPGurukul Park Ticketing Management System. The vulnerability allows remote attackers to inject arbitrary JavaScript code via the `fromdate` and `todate` parameters in a POST request, leading to code execution in the context of the victim's browser.

---

## **Steps to Reproduce**
1. **Log in to the Admin Panel**  
   - Access the admin login page and authenticate with valid credentials.
   ![image](https://github.com/user-attachments/assets/bb03345c-1628-499c-81ad-6563337ecdd3)
  
2. **Navigate to the Report Section**  
   - Go to the "Report" section and select "Foreigners People Report."
   ![image](https://github.com/user-attachments/assets/0e82e40c-9416-446d-bf8e-f9e4073626e1)

3. **Intercept the Request**  
   - Use Burp Suite to intercept the POST request containing the `fromdate` and `todate` parameters.
   ![image](https://github.com/user-attachments/assets/b286da72-2b9e-4730-8439-fd2640b941a7)
  
4. **Inject XSS Payload**  
   - Modify the parameters with the following payloads:  
     - `fromdate`: `<script>alert(1)</script>`  
     - `todate`: `<script>alert(2)</script>`
   - ![image](https://github.com/user-attachments/assets/3f302fed-e85b-43d8-afc6-1e2d91c568cc)

5. **Observe the Result**  
   - The injected script executes when the page renders the manipulated input.
     ![image](https://github.com/user-attachments/assets/7f217dd9-76ee-4474-bc63-bfc0f41c7019)
     ![image](https://github.com/user-attachments/assets/ca72929d-f89f-4c06-b0ff-9918a9e3f7f2)



## **Mitigation Recommendations**
- Implement input validation and output encoding for user-supplied data.  
- Use security libraries like HTMLPurifier to sanitize inputs.  
- Follow OWASP guidelines for XSS prevention:  
  - [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
- Refer to PortSwigger's XSS mitigation guide:  
  - [PortSwigger XSS Guide](https://portswigger.net/web-security/cross-site-scripting)  

---

## **References**
- [PHPGurukul Official Website](https://phpgurukul.com/)  
- [OWASP XSS Prevention](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
