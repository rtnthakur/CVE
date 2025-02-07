# Reflected Cross-Site Scripting (XSS) in MODX CMS

## Vulnerability Overview

| **Category**         | **Details**                              |
|-----------------------|------------------------------------------|
| **Product Name**      | MODX CMS                                 |
| **Product URL**       | [https://modx.com](https://modx.com)     |
| **Affected Versions** | MODX 3.1.0                               |
| **Vulnerability Type**| Reflected Cross-Site Scripting (XSS)     |
| **Component**         | Profile Image Upload Feature             |
| **Severity**          | High                                     |

## Vulnerability Description

A cross-site scripting (XSS) vulnerability has been identified in MODX versions prior to 3.1.0. The vulnerability allows authenticated users to upload SVG files containing malicious JavaScript code as profile images, which gets executed in victims' browsers when viewing the profile image.

## Problem Description

The application allows users to upload SVG files as profile images without proper sanitization. SVG files can contain embedded JavaScript code that executes when the image is rendered in a browser. This creates an XSS vulnerability where malicious code can be executed in the context of other users' sessions.

## Technical Impact

- Allows execution of arbitrary JavaScript code in victims' browsers.
- Potential theft of session tokens and sensitive data.
- Ability to perform unauthorized actions on behalf of the victim.
- Possible escalation to more severe attacks through initial JavaScript execution.

## Attack Vectors

- Attackers upload a specially crafted SVG file as their profile image.
- The SVG file contains embedded JavaScript code.
- When other users view the attacker's profile or any page displaying the profile image, the malicious code executes.

## Proof of Concept

### Steps to Reproduce

1. **Access the Admin Panel**
   - Navigate to: [http://localhost/modx/manager/](http://localhost/modx/manager/)
   - Log in with valid credentials.
   ![image](https://github.com/user-attachments/assets/d433e893-934c-4d26-a89f-016c13b96cdf)

2. **Upload a Malicious SVG**
   - Click on the upload button and choose the file option.
   - Select and upload a malicious SVG file.
   ![image](https://github.com/user-attachments/assets/4866b07c-0162-4d2e-8b72-965bb546789b)

   - Click the upload button. The file is uploaded successfully without detection.
   ![image](https://github.com/user-attachments/assets/8ecb40db-9b30-422e-b4ab-cf7d3f3d59ad)
   ![image](https://github.com/user-attachments/assets/55b95fd2-a897-4cef-ac83-9a73edbf2167)

3. **Open the Profile Image in a New Tab**
   - Click on the profile icon and open it in a new tab.
   ![image](https://github.com/user-attachments/assets/339d8f3b-4804-443c-9fd2-476770c97af0)

4. **Observe the Execution of the Injected JavaScript Payload**
   - The malicious JavaScript code executes in the browser.
   ![image](https://github.com/user-attachments/assets/a16cee66-80ce-4ce1-a8cc-bd0fb1dc0d34)

## Impact

- Execution of arbitrary JavaScript in the context of the admin's browser.
- Potential to steal admin cookies, hijack sessions, or perform actions on behalf of the admin.

## Recommended Actions

1. **Input Validation**: Enforce strict validation to block harmful scripts or tags.
2. **Output Encoding**: Encode user inputs before rendering.
3. **Content Security Policy (CSP)**: Use a strong CSP to block unauthorized scripts.
4. **Upgrade**: Update MODX CMS to a patched version if available.

## References

- [OWASP XSS Prevention Cheat Sheet](https://owasp.org)
