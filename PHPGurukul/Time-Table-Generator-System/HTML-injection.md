# HTML Injection Vulnerability Report

## Vulnerability Overview

HTML Injection was discovered in the `profile.php` file of the **PHPGurukul Timetable Generator System Project in PHP v1.0**. This vulnerability allows remote attackers to execute arbitrary HTML code through the `adminname` POST request parameter.

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
| Affected File       | `profile.php`                                                           |
| Affected Parameter  | `adminname`                                                             |
| Request Method      | POST                                                                    |
| Vulnerability Type  | HTML Injection                                                          |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**:
   - Open the admin login page.
   - Enter valid credentials and sign in.
   ![image](https://github.com/user-attachments/assets/abd0503c-9d3d-4354-8845-106e7897ff22)

2. **Navigate to Profile Section**:
   - Go to the “superadmin” section.
   - Click the “Profile” button.
   ![image](https://github.com/user-attachments/assets/8d100d16-5600-4c7c-ad0b-88107a238c0e)
   
   - Make any necessary changes.
   - Click the “Update” button.
   ![image](https://github.com/user-attachments/assets/a90d7e76-d1ff-4dee-95ce-09b89c901590)

3. **Intercept the Request**:
   - Launch Burp Suite and configure your browser to route traffic through it.
   - Enable Burp Suite Interceptor to capture the HTTP request.
   ![image](https://github.com/user-attachments/assets/26c74f21-6e27-47b1-8a75-764f9a1f8f31)

4. **Modify the Request**:
   - Capture the request when updating user details.
   - Send the request to Burp Suite Repeater.
   - Modify the `adminname` parameter with the following payload:
     ```html
     (<h1>Hello</h1)
     ```
   - ![image](https://github.com/user-attachments/assets/590c47c4-f060-42be-b264-cd470bfb8fca)


5. **Send and Observe**:
   - Send the modified request.
   - The injected HTML (`<h1>Hello</h1>`) is rendered on the page, confirming HTML Injection.
   ![image](https://github.com/user-attachments/assets/902d9e51-2c26-422a-ab98-945ce2fb3493)

---

## Recommended Mitigations

- Implement proper input validation.
- Apply output encoding to user-supplied data.
- Utilize a Content Security Policy (CSP) to mitigate the risk of malicious HTML injection.

