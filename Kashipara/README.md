# Stored Cross-Site Scripting (XSS) in Online Attendance Management System V1.0

## Overview
A Stored Cross-Site Scripting (XSS) vulnerability was discovered in the `manage-employee.php` page of the Kashipara Online Attendance Management System project V1.0. This vulnerability allows remote attackers to execute arbitrary scripts via the `department` parameter in the `/attendance/admin/manage-employee.php` URL.

## Official Website
- **Official Website URL**: [Kashipara Online Attendance Management System](https://www.kashipara.com/project/php/13168/online-attendance-management-system-php-project-source-code)

## Affected Product
| **Detail**               | **Value**                              |
|--------------------------|----------------------------------------|
| **Product Name**         | Online Attendance Management System    |
| **Vendor**               | Kashipara                              |
| **Version**              | V1.0                                   |

## Vulnerability Details
| **Detail**               | **Value**                              |
|--------------------------|----------------------------------------|
| **Affected Code File**   | `/attendance/admin/manage-employee.php`|
| **Affected Parameter**   | `department`                           |
| **Method**               | POST                                   |
| **Type**                 | Stored Cross-Site Scripting (XSS)      |

## Description
A stored XSS vulnerability exists in the Online Attendance Management System version V1.0. An attacker can inject malicious scripts via the `department` field in the "Manage Employee" section of the Admin Panel. The malicious payload executes when the admin reviews the comments, potentially compromising the admin account and the underlying application.

## Steps to Reproduce
1. **Access the Target Application**:
   - Navigate to the admin dashboard: `http://localhost/kasipara/attendance/admin/dashboard.php`
   - Log in with valid credentials.
   - Click on the **NO OF STAFF** area.
   - ![image](https://github.com/user-attachments/assets/3fae569e-fe92-44d3-8396-6aa7b3f9b52f)

2. **Switch to the Manage Employee Section**:
   - Click on the number of staff area to access the Manage Employees section.
   - Click on the **Edit** button.
    ![image](https://github.com/user-attachments/assets/34b9cdbc-da6a-4390-a266-b336274c78d3)

3. **Navigate to the Edit Page**:
   - Fill in all required fields on the edit employee page.
     ![image](https://github.com/user-attachments/assets/7673d3f7-4060-4a34-a180-cca1e570969e)

4. **Intercept the Request**:
   - Enable Burp Suite and set up the browser to route traffic through it.
    ![image](https://github.com/user-attachments/assets/bb0a3181-fa37-4c9b-95de-277a24edd5e3)

5. **Modify the Parameter**:
   - Send the request to the Burp Suite Repeater.
   - Modify the `department` parameter with the payload: `<script>alert(1)</script>`.
     ![image](https://github.com/user-attachments/assets/07a3381e-2a68-46a9-a0e9-037c7e39bf7d)

6. **Send the Modified Request**:
   - Forward the modified request in the Burp Suite Repeater.
   - Observe the delay in the response code.
     ![image](https://github.com/user-attachments/assets/de1f19bf-3fb7-4e56-94e9-c7de009183b2)

7. **Trigger the Payload**:
   - Navigate to the "ACTION" section in the Manage Employee.
   - Observe the stored payload in the `department` parameter.
     ![image](https://github.com/user-attachments/assets/ddd5c3d5-dd5b-4bdd-a5e1-39275f5f7292)

   - Click the **View** button to execute the injected JavaScript payload.
     ![image](https://github.com/user-attachments/assets/24daf537-353c-41fe-8a28-0c5cca23b7d4)

## Impact
- Execution of arbitrary JavaScript in the context of the admin's browser.
- Potential to steal admin cookies, hijack sessions, or perform actions on behalf of the admin.

## Recommendations
- **Input Validation**: Enforce strict validation to block harmful scripts or tags.
- **Output Encoding**: Encode user inputs before rendering.
- **Content Security Policy (CSP)**: Use a strong CSP to block unauthorized scripts.

## References
- [OWASP XSS Prevention Cheat Sheet](https://owasp.org)

## Reported By
- **Name**: Ratnesh Kumar
- **Email**: ratanthakur740@gmail.com
