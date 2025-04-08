# Stored Cross-Site Scripting (XSS) Vulnerability in PHPGurukul Directory Management System v2.0

## Vulnerability Summary
A critical **Stored Cross-Site Scripting (XSS)** vulnerability was discovered in the `/DMS/dms/admin/search-directory.php` file of PHPGurukul's Directory Management System (v2.0). Attackers can inject malicious scripts via the `searchdata` POST parameter, which are then persistently stored and executed when the search functionality is used.

### Key Details
| **Property**          | **Value**                              |
|-----------------------|----------------------------------------|
| Affected Vendor       | Phpgurukul                             |
| Vulnerable File       | `search-directory.php`                 |
| Attack Vector         | `searchdata` parameter (POST request)  |
| Vulnerability Type    | Stored XSS                             |
| Version Affected      | v2.0                                   |
| Official Website      | [PHPGurukul DMS](https://phpgurukul.com/directory-management-system-using-php-and-mysql/) |

---

## Proof of Concept (PoC)

### Step-by-Step Exploitation
1. **Admin Panel Login**  
   - Authenticate to the admin portal using valid credentials.  
   ![image](https://github.com/user-attachments/assets/41d9f635-c5d1-40fe-b0af-d9e99011b281)
  
2. **Navigate to Search Directory**  
   - Access the "Search Directory" section from the dashboard.  
   ![image](https://github.com/user-attachments/assets/38261406-36f4-445f-8a2f-8a4e733bd1ed)
  
3. **Intercept Search Request**  
   - Configure Burp Suite (`127.0.0.1:8080`) to intercept the POST request.  
   - Enable the **Interceptor** in Burp's Proxy tab.  
   ![image](https://github.com/user-attachments/assets/0de9c554-5e5b-41a7-bd03-fc859869a6e2)
  
4. **Inject Malicious Payload**  
   - Capture the request and modify the `searchdata` parameter with:  
     ```html
     <script>alert(1)</script>
     ```
   - ![image](https://github.com/user-attachments/assets/60f97c1c-fc6b-4ed4-bff6-fa6c72b50654)

5. **Execute and Observe**  
   - The injected script renders persistently, triggering an alert when the search page is reloaded.  
   ![image](https://github.com/user-attachments/assets/8d7105bc-8c4e-483d-aaf7-fcb38e53ada3)
  
---

## Potential Impact
- **Session Hijacking**: Steal admin cookies or session tokens.  
- **Phishing Attacks**: Inject fake login forms to harvest credentials.  
- **Defacement**: Modify displayed content to spread misinformation.  
- **Malware Distribution**: Redirect users to malicious sites.  

---

## Mitigation Strategies
1. **Input Sanitization**  
   - Use libraries like `htmlspecialchars()` or DOMPurify to neutralize HTML/JS in user inputs.  
2. **Content Security Policy (CSP)**  
   - Implement CSP headers to restrict inline scripts and unauthorized sources.  
3. **Output Encoding**  
   - Encode dynamic content before rendering (e.g., via OWASP’s ESAPI).  
4. **Framework Protections**  
   - Leverage modern PHP frameworks (e.g., Laravel, Symfony) with built-in XSS protections.  

### Recommended Resources
- [PortSwigger XSS Guide](https://portswigger.net/web-security/cross-site-scripting)  
- [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  

---

**Urgency**: Patch immediately to prevent exploitation in production environments.  
