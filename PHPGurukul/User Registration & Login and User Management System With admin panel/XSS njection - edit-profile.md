# Reflected Cross-Site Scripting (XSS) - `fname`, `lname`, `contact` Parameters

A **Reflected Cross-Site Scripting (XSS)** vulnerability was found in `loginsystem/edit-profile.php` of the **PHPGurukul User Registration & Login and User Management System V3.3**. This vulnerability allows remote attackers to execute arbitrary JavaScript code via the `fname`, `lname`, and `contact` parameters in a **POST HTTP request**.

## Official Website URL  
[PHPGurukul - User Registration & Login and User Management System](https://phpgurukul.com/user-registration-login-and-user-management-system-with-admin-panel/)

## Affected Product Details  

| **Field**            | **Details** |
|----------------------|------------|
| **Product Name**    | User Registration & Login and User Management System With Admin Panel |
| **Vendor**         | PHPGurukul |
| **Affected Code File** | `loginsystem/edit-profile.php` |
| **Affected Parameters** | `fname`, `lname`, `contact` |
| **Method**         | `POST` |
| **Type**          | Cross-Site Scripting (XSS) |
| **Version**       | V3.3 |

---

## Steps to Reproduce

### 1. Log in to the Admin Panel:
- Open the admin login page.
- Enter your credentials and sign in.
![image](https://github.com/user-attachments/assets/bb0ce478-b198-47ec-a342-adc861ce42ef)

### 2. Go to Manage Users:
- Navigate to the **Manage Users** section.
- Find a user and click the **Edit** button.
![image](https://github.com/user-attachments/assets/3b0695e3-9b37-4e6b-91d8-1518c80fa3bd)

- Make any changes if needed.
- Click **Update**.
![image](https://github.com/user-attachments/assets/7a8259ec-71a5-4904-a571-edf615a84961)

### 3. Intercept the Request:
- Launch **Burp Suite** and configure your browser to route traffic through it.
- Enable **Burp Suite Interceptor** to capture requests.
![image](https://github.com/user-attachments/assets/5232358c-07fc-4261-ab66-73ca708fef0e)

### 4. Modify the Request:
- Capture the request when updating user details.
- Send it to the **Burp Suite Repeater**.
- Modify the `fname`, `lname`, and `contact` parameters by injecting this payload:
  ```html
  <script>alert(1)</script>
  ```
- ![image](https://github.com/user-attachments/assets/05057879-de37-4dcc-a3f0-ec737d4ccc3f)

### 5. Send and Observe:
- The injected XSS payload is executed on the page.
![image](https://github.com/user-attachments/assets/0b658539-880f-4a1b-9b85-ef315fa109cb)

---

## Mitigation & Recommendations  
- [PortSwigger - Cross-Site Scripting (XSS)](https://portswigger.net/web-security/cross-site-scripting)  
- [OWASP - XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
