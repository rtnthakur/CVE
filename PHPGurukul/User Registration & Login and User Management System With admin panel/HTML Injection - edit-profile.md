# HTML Injection - `fname`, `lname`, `contact` Parameters

A **HTML Injection** vulnerability was found in `loginsystem/edit-profile.php` of the **PHPGurukul User Registration & Login and User Management System V3.3**. This vulnerability allows remote attackers to execute arbitrary HTML code via the `fname`, `lname`, and `contact` parameters in a **POST HTTP request**.

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
| **Type**          | HTML Injection |
| **Version**       | V3.3 |

---

## Steps to Reproduce

### 1. Log in to the Admin Panel:
- Open the admin login page.
- Enter your credentials and sign in.
![image](https://github.com/user-attachments/assets/c666371a-b75d-41fb-8a21-eb70992cd6b6)

### 2. Go to Manage Users:
- Navigate to the **Manage Users** section.
- Find a user and click the **Edit** button.
![image](https://github.com/user-attachments/assets/c335a295-f8ab-4be4-90a9-57acf9f3d4df)

- Make any changes if needed.
- Click **Update**.
![image](https://github.com/user-attachments/assets/c6dfa1e3-a30d-4830-9e25-0a2436054c28)


### 3. Intercept the Request:
- Launch **Burp Suite** and configure your browser to route traffic through it.
- Enable **Burp Suite Interceptor** to capture requests.
![image](https://github.com/user-attachments/assets/4a0cc55c-0377-4f4b-a6a5-d275cfe21b28)

### 4. Modify the Request:
- Capture the request when updating user details.
- Send it to the **Burp Suite Repeater**.
- Modify the `fname`, `lname`, and `contact` parameters by injecting this payload:
  ```html
  <<h1>Hello</h1>
  ```
![image](https://github.com/user-attachments/assets/442da994-d30e-4fa8-bc3a-2678ed4fb954)


### 5. Send and Observe:
- The injected HTML is rendered on the page.
![image](https://github.com/user-attachments/assets/b3528623-bfe5-4fe4-8ef8-2a79d36fa2da)

---

## Mitigation & Recommendations  
- Implement **proper input validation** to sanitize user inputs.
- Apply **output encoding** to prevent malicious HTML injection.
- Use **Content Security Policy (CSP)** to restrict allowed content.

