# SQL Injection Vulnerability in Dairy Farm Shop Management System

## Overview
A SQL injection vulnerability was discovered in the PHPGurukul Dairy Farm Shop Management System (Version 1.3). The vulnerability allows remote attackers to execute arbitrary SQL code via the `category` and `categorycode` parameters in a POST request to the `manage-categories.php` file.

**Official Website**: [Dairy Farm Shop Management System](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)

---

## Vulnerability Details
| **Field**           | **Details**                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| Affected Vendor     | Phpgurukul                                                                 |
| Affected Code File  | `manage-categories.php`                                                    |
| Affected Parameters | `category` and `categorycode`                                              |
| Method              | POST                                                                       |
| Type                | Time-based blind SQL injection                                            |
| Version             | V1.3                                                                      |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**
   - Navigate to the admin login page.
   - Enter valid credentials and sign in.
    ![image](https://github.com/user-attachments/assets/aadaf405-5ee9-4994-8cb6-83fdbb9924d5)

2. **Navigate to the Category Section**
   - Click the "manage" button to edit a category.
   - Fill in any value in the input field.
    ![image](https://github.com/user-attachments/assets/88d5d00d-ce68-4b6f-800d-230def6b2554)

3. **Intercept the Request**
   - Launch Burp Suite and configure the browser to route traffic through it.
   - Enable Burp Suite Interceptor to capture the request.
    ![image](https://github.com/user-attachments/assets/aa093a04-c54d-41fa-9743-5282a89750c3)

4. **Modify the Request**
   - Capture the request when updating user details.
   - Send it to Burp Suite Repeater.
   - Modify the `category` and `categorycode` parameters with the payload:  
     `'%2b(select*from(select(sleep(10)))a)%2b'`
   ![image](https://github.com/user-attachments/assets/3519fc9b-cd78-48f5-9c25-fab5a5ba75b8)

5. **Send the Modified Request**
   - Forward the request in Burp Suite Repeater.
   - Observe the delayed response (10 seconds), confirming the SQL injection vulnerability.
   ![image](https://github.com/user-attachments/assets/32e41ce9-12f7-401e-a9b9-ba6bc02b7ce1)


---

## Impact
- **Data Theft**: Unauthorized access to sensitive data in the database.
- **Data Manipulation**: Alteration or deletion of data, compromising integrity.
- **Reconnaissance**: Enumeration of database structure for further exploitation.
- **Financial Loss**: Potential service disruption leading to monetary losses.
- **Reputation Damage**: Loss of user trust due to data breaches or service outages.

---

## Recommended Mitigations
- Implement **input validation** and **output encoding**.
- Use **prepared statements** or **parameterized queries**.
- Apply the principle of **least privilege** for database access.
- Deploy a **Content Security Policy (CSP)** to mitigate injection risks.

**Reference**: [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

--- 

**Note**: The screenshots referenced in the original document are omitted in this markdown version for brevity. Ensure to include them in the final report if needed.
