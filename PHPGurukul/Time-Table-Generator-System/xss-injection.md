# Reflected Cross-Site Scripting (XSS) Vulnerability Report

## Vulnerability Overview

A Reflected Cross-Site Scripting (XSS) vulnerability was discovered in the `profile.php` file of the **PHPGurukul Timetable Generator System Project in PHP v1.0**. This vulnerability allows remote attackers to execute arbitrary JavaScript code via the `adminname` POST request parameter.

---

## Official Website

[https://phpgurukul.com/time-table-generator-system-using-php-and-mysql/](https://phpgurukul.com/time-table-generator-system-using-php-and-mysql/)

---

## Affected Product

| Field               | Details                                                                 |
|---------------------|-------------------------------------------------------------------------|
| Product Name        | Timetable Generator System using PHP and MySQL                         |
| Version             | v1.0                                                                    |
| Vendor              | PHPGurukul                                                              |
| Affected File       | `profile.php`                                                      |
| Affected Parameter  | `adminname`                                                             |
| Request Method      | POST                                                                    |
| Vulnerability Type  | Reflected Cross-Site Scripting (XSS)                                    |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**:
   - Open the admin login page.
   - Enter valid credentials and sign in.
   - <img width="952" alt="Screenshot_1" src="https://github.com/user-attachments/assets/39d65389-2293-4966-aace-a2a492b48d17" />

2. **Navigate to Manage Profile**:
   - Go to the “superadmin” section.
   - Click the “Profile” button.
   ![image](https://github.com/user-attachments/assets/85cc721f-e117-4886-a39b-6120cf989e4e)

   - Make any necessary changes.
   - Click the “Update” button.
  ![image](https://github.com/user-attachments/assets/2cf39a37-76b7-43a7-8f5f-13d58fd3bbd6)


3. **Intercept the Request**:
   - Launch Burp Suite and configure your browser to route traffic through it.
   - Enable Burp Suite Interceptor to capture the HTTP request.
   - ![image](https://github.com/user-attachments/assets/c5252c7a-9374-4849-a24b-d10b74031a07)

4. **Modify the Request**:
   - Capture the request when updating user details.
   - Send the request to Burp Suite Repeater.
   - Modify the `adminname` parameter with the following payload:
     ```html
     (<script>alert(1)</script>)
     ```
   - ![image](https://github.com/user-attachments/assets/2e1cf0ff-54fe-48ea-a896-5eccd4451ef5)

5. **Send and Observe**:
   - Send the modified request.
   - The injected JavaScript is executed, demonstrating XSS vulnerability.
   - ![image](https://github.com/user-attachments/assets/fa2e0075-dffe-4ce1-a0d6-63c72f07f0ff)

---

## Recommended Mitigations

- Follow secure coding practices and implement proper input validation and output encoding.
- Use appropriate HTTP response headers such as Content Security Policy (CSP).
- Refer to the following resources for mitigation strategies:
  - [PortSwigger XSS Guide](https://portswigger.net/web-security/cross-site-scripting)
  - [OWASP XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)

