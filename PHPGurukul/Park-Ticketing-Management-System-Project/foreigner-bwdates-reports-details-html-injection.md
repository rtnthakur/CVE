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
   ![image](https://github.com/user-attachments/assets/40b7665a-e900-481e-8979-6efb09c74f0d)

2. **Navigate to the Reports Section**  
   - Go to the "Report" section in the Admin Dashboard.  
   - Click on "Foreigners People Report".
   ![image](https://github.com/user-attachments/assets/52afa59e-ee2b-4aa0-b7e3-c722cc56bccf)
  
3. **Intercept the Request**  
   - Use **Burp Suite** to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
   ![image](https://github.com/user-attachments/assets/7f376d69-c14f-40cb-96d6-17b8db69d4f2)
 
4. **Modify the Request**  
   - Capture the request when submitting date range details.  
   - Forward it to the Burp Suite Repeater.  
   - Inject the following payload into either `fromdate` or `todate` parameter:  
     ```html
     <h1>Hello</h1>
     ```
   - ![image](https://github.com/user-attachments/assets/361a5ea1-a123-4bc5-86f7-534797d73a0a)


5. **Send and Observe**  
   - The injected HTML will be rendered on the page, confirming the vulnerability.
   ![image](https://github.com/user-attachments/assets/8c7bbb0a-1f02-4257-acae-e072bc9c5e95)
  

---

## Recommended Mitigations
- **Input Validation**: Implement strict input validation to filter malicious payloads.  
- **Output Encoding**: Encode output to prevent HTML/JavaScript execution.  
- **Content Security Policy (CSP)**: Deploy CSP headers to mitigate injection risks.  

---

**Security Note**: This vulnerability could potentially lead to more severe attacks if exploited. It is recommended to apply these security measures immediately and conduct regular security audits to ensure the system's integrity.
