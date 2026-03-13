## Lab Name
Unprotected Admin Functionality with Unpredictable URL

## Platform
PortSwigger Web Security Academy

## Vulnerability
Access Control Vulnerability – Unprotected Admin Functionality

## Objective
Access the hidden admin panel and delete the user **carlos**.

## Entry Point
Admin panel URL exposed inside a JavaScript file.

## Exploitation Type
Direct access to unprotected administrative functionality using a hidden endpoint.

## Methodology
1. Opened the lab and started exploring the website normally.
2. Checked the page source and loaded JavaScript files used by the application.
3. Discovered a JavaScript file that contained a hidden admin URL.
4. Observed a path similar to '/admin-<random-string>' inside the JavaScript code.
5. Copied the discovered admin path and accessed it directly in the browser.
6. The admin interface opened without any authentication.
7. Located the option to manage users.
8. Deleted the user **carlos** from the admin panel to solve the lab.

### JavaScript File Discovery
/js/<script-file>.js

### Hidden Admin Endpoint
/admin-<random-string>

### Action Performed
Delete user: carlos

## Result
Successfully accessed the hidden **administrator panel** using the unpredictable URL and deleted the user **carlos**, which solved the lab.

## Impact
If administrative functionality is only protected by hiding the URL, attackers can still discover it through:

- JavaScript files
- Source code inspection
- Directory brute forcing
- Application leaks

This can allow attackers to:
- Access admin panels
- Delete or modify users
- Manipulate application data
- Gain full control of the system

## Mitigation
- Implement proper authentication and authorization for admin endpoints.
- Do not rely on hidden or unpredictable URLs for security.
- Use role-based access control (RBAC).
- Restrict admin functionality on the server side.
- Avoid exposing sensitive endpoints in client-side code.

## Learning
Security through obscurity is not a secure defense. Even if the admin URL is unpredictable, attackers can discover it through client-side files such as JavaScript. Proper authentication and authorization must always be enforced for administrative functionality.
