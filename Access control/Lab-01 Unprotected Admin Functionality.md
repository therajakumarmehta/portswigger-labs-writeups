## Lab Name
Unprotected Admin Functionality

## Platform
PortSwigger Web Security Academy

## Vulnerability
Access Control Vulnerability – Unprotected Admin Functionality

## Objective
Access the admin panel and delete the user **carlos**.

## Entry Point
Hidden admin panel discovered via **robots.txt**

## Exploitation Type
Direct access to unprotected administrative functionality

## Methodology
1. Opened the lab and started exploring the website functionality.
2. Checked common files such as **robots.txt** to find hidden directories.
3. Discovered a hidden admin directory mentioned inside the robots.txt file.
4. Accessed the exposed admin panel directly through the discovered path.
5. Observed that the admin interface was accessible without authentication.
6. Located the option to manage users inside the admin panel.
7. Deleted the user **carlos** to solve the lab.

## Payload 
/ Endpoint Used

### Discover Hidden Path
/robots.txt

### Access Admin Panel
/administrator-panel

### Action Performed
Delete user: carlos

## Result
Successfully accessed the **administrator panel without authentication** and deleted the user **carlos**, which solved the lab.

## Impact
An attacker can gain unauthorized access to administrative functionality and perform critical actions such as:

- Deleting users
- Modifying data
- Accessing sensitive information
- Taking full control of the application

## Mitigation
- Protect admin endpoints with proper authentication.
- Implement role-based access control (RBAC).
- Restrict access to administrative functionality on the server side.
- Avoid exposing sensitive directories in robots.txt.
- Monitor and log access to critical endpoints.

## Learning
Sensitive administrative functionality must always require proper authentication and authorization. Hidden paths or directories are not a secure method of protecting admin panels, as attackers can easily discover them using files like **robots.txt** or through enumeration techniques.
