# HTML Injection - `searchkey` Parameter

A **HTML Injection** vulnerability was found in the `/search-result.php` page of the **PHPGurukul User Registration & Login and User Management System V3.3**. This vulnerability allows remote attackers to execute arbitrary HTML code via the `searchkey` parameter in a **POST HTTP request**.

## Official Website URL  
[PHPGurukul - User Registration & Login and User Management System](https://phpgurukul.com/user-registration-login-and-user-management-system-with-admin-panel/)

## Affected Product Details  

| **Field**            | **Details** |
|----------------------|------------|
| **Product Name**    | User Registration & Login and User Management System With Admin Panel |
| **Vendor**         | PHPGurukul |
| **Affected Code File** | `/admin/search-result.php` |
| **Affected Parameter** | `searchkey` |
| **Method**         | `POST` |
| **Type**          | HTML Injection |
| **Version**       | V3.3 |

---

## Steps to Reproduce

1. **Click on Admin login.**  
![image](https://github.com/user-attachments/assets/b3c7a485-76b7-455c-86a0-78a82965f57b)

2. **Login with valid credentials.**  
![image](https://github.com/user-attachments/assets/6062ff9f-e7fb-4f38-b292-70423a88a512)

3. **Locate the search bar, type the HTML payload:**  
   ```html
   <h1>Hello</h1>
   ```
   and enable **Burp Suite** to confirm the parameter.  
![image](https://github.com/user-attachments/assets/0ac8e0c9-5992-43ac-94a9-2c707512b278)

4. **In Burp Suite**, look at the intercepted request and make sure it contains:  
   ```
   searchkey=<h1>Hello</h1>
   ```
   If everything looks good, click **"Forward"** to send it to the server.  
![image](https://github.com/user-attachments/assets/4c20f7c5-d9dd-4aac-bef7-20cfeeda3e45)

5. **Observe in the browser** as the payload executes, rendering the HTML element.  
![image](https://github.com/user-attachments/assets/37b04315-a16e-48ff-8917-2b7b54aa5703)

---

## Mitigation & Recommendations  

- [OWASP - Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Injection_Prevention_Cheat_Sheet.html)  
- [Stack Overflow - Preventing HTML and Script Injections in JavaScript](https://stackoverflow.com/questions/20855482/preventing-html-and-script-injections-in-javascript)  
