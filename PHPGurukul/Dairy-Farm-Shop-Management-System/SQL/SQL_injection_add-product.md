# SQL Injection Vulnerability in Dairy Farm Shop Management System (Add Product)

## Overview
A SQL injection vulnerability was identified in the PHPGurukul Dairy Farm Shop Management System (version 1.3). The vulnerability allows remote attackers to execute arbitrary SQL code via the `category`, `company`, `productname`, and `productprice` parameters in a POST request to `add-product.php`.

### Affected Product Details
- **Product Name**: Dairy Farm Shop Management System  
- **Vendor**: Phpgurukul  
- **Official Website**: [https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/](https://phpgurukul.com/dairy-farm-shop-management-system-using-php-and-mysql/)  

| Affected Component      | Details                                                                 |
|-------------------------|-------------------------------------------------------------------------|
| Affected Code File      | `add-product.php`                                                      |
| Affected Parameters     | `category`, `company`, `productname`, `productprice` (POST request)    |
| Vulnerability Type      | Time-based blind SQL injection                                         |
| Version Affected        | V1.3                                                                   |

---

## Steps to Reproduce

1. **Log in to the Admin Panel**  
   - Access the admin login page.  
   - Enter valid credentials to sign in.
    ![image](https://github.com/user-attachments/assets/59a2bcaa-4ee1-4ade-b7f1-ae0d019f5d3d)

2. **Navigate to the Product Section**  
   - Click the "Add" button to add a new product.  
   - Fill in any values in the input fields.
   ![image](https://github.com/user-attachments/assets/2ae551a1-39c7-46e9-8def-40d17e78595e)
   
3. **Intercept the Request**  
   - Use Burp Suite to capture the request.  
   - Enable the Burp Suite Interceptor to monitor traffic.
   ![image](https://github.com/user-attachments/assets/56904403-e34c-4e9d-9c68-d66f9b559c84)
   
4. **Modify the Request**  
   - Capture the request when submitting product details.  
   - Send it to Burp Suite Repeater.  
   - Inject the following payload into any of the affected parameters (`category`, `company`, `productname`, or `productprice`):  
     ```sql
     '%2b(select*from(select(sleep(10)))a)%2b'
     ```
  - ![image](https://github.com/user-attachments/assets/e2e9e1fd-c874-40fd-bce1-81d566f4a408)

5. **Confirm the Vulnerability**  
   - Forward the modified request.  
   - Observe a 40-second delay in the response, confirming the time-based SQL injection.
  - ![image](https://github.com/user-attachments/assets/fc8e4c2b-3706-4409-8115-31d7b7fbdf5e)

---

## Impact
- **Data Theft**: Unauthorized access to sensitive database information.  
- **Data Manipulation**: Alteration or deletion of critical data.  
- **Reconnaissance**: Enumeration of database structures for further attacks.  
- **Financial Loss**: Potential service disruption leading to monetary damages.  
- **Reputation Damage**: Loss of user trust due to security breaches.  

---

## Recommended Mitigations
1. **Input Validation**: Sanitize and validate all user inputs.  
2. **Prepared Statements**: Use parameterized queries to prevent SQL injection.  
3. **Output Encoding**: Encode data before rendering it in the application.  
4. **Content Security Policy (CSP)**: Implement CSP to mitigate HTML injection risks.  

For detailed guidance, refer to the [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html).  

---

**Note**: Screenshots referenced in the original document are omitted in this markdown version for brevity.  
