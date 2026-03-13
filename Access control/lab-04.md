## Lab Name
User role can be modified in user profile

## Platform
PortSwigger Web Security Academy

## Vulnerability
Access Control Vulnerability – Privilege Escalation via User Profile Modification

## Objective
Gain administrator privileges and delete the user **carlos**.

## Entry Point
User profile update functionality

## Exploitation Type
Parameter Tampering / Privilege Escalation

## Methodology
1. Opened the lab and logged in with the provided user credentials.
2. Navigated to the **user profile** page where profile information could be updated.
3. Intercepted the profile update request using **Burp Suite Proxy**.
4. Observed that the request contained parameters related to the user account.
5. Identified a parameter controlling the user role (e.g., 'roleid').
6. Modified the role parameter from a normal user role to an administrator role.
7. Forwarded the modified request to the server.
8. The application updated the account with administrator privileges.
9. Accessed the **admin panel** and deleted the user **carlos**.

## Payload / Parameter Used

### Original Request
roleid=1

### Modified Request
roleid=2

## Result
Successfully escalated privileges to **administrator** by modifying the role parameter in the user profile request and deleted the user **carlos**, solving the lab.

## Impact
If user roles can be modified through profile update requests, attackers can escalate privileges and gain unauthorized administrative access. This may allow attackers to:

- Access the admin panel
- Delete or modify users
- Access sensitive data
- Take full control of the application

## Mitigation
- Do not allow role or privilege parameters to be modified by normal users.
- Implement strict **server-side access control checks**.
- Validate and restrict sensitive parameters in profile update requests.
- Use role-based access control (RBAC) and verify permissions on the server.

## Learning
User privilege levels should never be controlled or modified through client-accessible parameters. Sensitive attributes such as **user roles** must be securely handled and validated on the server side to prevent privilege escalation attacks.
