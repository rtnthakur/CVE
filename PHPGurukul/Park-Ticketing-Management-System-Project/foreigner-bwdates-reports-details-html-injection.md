# HTML Injection Vulnerability in Park Ticketing Management System (Foreigner Date Range Report)

## Overview
An HTML Injection vulnerability was discovered in the `foreigner-bwdates-reports-details.php` file of the **Park Ticketing Management System Project in PHP v2.0** by PHPGurukul. This vulnerability allows remote attackers to execute arbitrary code via the `fromdate` and `todate` POST request parameters.

- **Official Website**: [PHPGurukul Park Ticketing Management System](https://phpgurukul.com/park-ticketing-management-system-using-php-and-mysql/)
- **Affected Product**: Park Ticketing Management System Using PHP and MySQL

---

## Vulnerability Details

| Category              | Details                                                                 |
|-----------------------|-------------------------------------------------------------------------|
| Vendor                | PHPGurukul                                                             |
| Affected Component    | `foreigner-bwdates-reports-details.php`                                |
| Vulnerable Parameters | `fromdate`, `todate`                                                   |
| Attack Vector         | POST Request                                                           |
| Vulnerability Type    | HTML Injection                                                         |
| Impact                | Arbitrary HTML/JavaScript Execution                                    |
| Affected Version      | v2.0                                                                   |
| CWE ID                | CWE-79: Improper Neutralization of Input During Web Page Generation    |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.  

2. **Navigate to the Reports Section**  
   - Go to the "Report" section in the Admin Dashboard.  
   - Click on "Foreigners People Report".  

3. **Intercept the Request**  
   - Use **Burp Suite** to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.  

4. **Modify the Request**  
   - Capture the request when submitting date range details.  
   - Forward it to the Burp Suite Repeater.  
   - Inject the following payload into either `fromdate` or `todate` parameter:  
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

**Security Note**: This vulnerability could potentially lead to more severe attacks if exploited. It is recommended to apply these security measures immediately and conduct regular security audits to ensure the system's integrity.
