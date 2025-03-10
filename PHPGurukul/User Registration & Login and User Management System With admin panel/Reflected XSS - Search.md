# Reflected Cross-Site Scripting (XSS) - `searchkey` Parameter

A **Reflected Cross-Site Scripting (XSS)** vulnerability was found in the `/search-result.php` page of the **PHPGurukul User Registration & Login and User Management System V3.3**. This vulnerability allows remote attackers to execute arbitrary scripts via the `searchkey` parameter in a **POST HTTP request**.

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
| **Type**          | Reflected XSS |
| **Version**       | V3.3 |

---

## Steps to Reproduce

1. **Click on Admin login.**  
![image](https://github.com/user-attachments/assets/3ad76218-7b8e-469f-a015-b929085aed3e)

2. **Login with valid credentials.**  
![image](https://github.com/user-attachments/assets/9d679a4a-9abf-4d67-aa0f-a4cff6e2d360)

3. **Locate the search bar, type the JavaScript payload:**  
   ```html
   <script>alert(1)</script>
   ```
   and enable **Burp Suite** to confirm the parameter.  
![image](https://github.com/user-attachments/assets/225cb28f-03cd-4a91-810a-7d793aa469a2)

4. **In Burp Suite**, look at the intercepted request and make sure it contains:  
   ```
   searchkey=<script>alert(1)</script>
   ```
   If everything looks good, click **"Forward"** to send it to the server.  
![image](https://github.com/user-attachments/assets/b7650420-846b-4a91-aaa4-20d23e2b937f)

5. **Observe in the browser** as the payload executes, triggering an alert popup.  
![image](https://github.com/user-attachments/assets/dd045fdd-dddf-45ea-9298-0546762ab200)

---

## Mitigation & Recommendations  

- [PortSwigger - Cross-Site Scripting (XSS)](https://portswigger.net/web-security/cross-site-scripting)  
- [OWASP - XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)  
