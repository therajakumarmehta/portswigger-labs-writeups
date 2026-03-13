## Lab Name
User role controlled by request parameter

## Platform
PortSwigger Web Security Academy

## Vulnerability
Access Control Vulnerability – Privilege Escalation via Request Parameter

## Objective
Delete the user **carlos** by gaining administrator privileges.

## Entry Point
'Admin' parameter in the HTTP request

## Exploitation Type
Parameter Manipulation (Privilege Escalation)

## Methodology
1. Opened the lab and logged in with the provided user credentials.
2. Intercepted the HTTP request using **Burp Suite Proxy**.
3. Observed that the request contained a parameter controlling user privileges.
4. The parameter 'Admin=false' indicated that the user did not have administrative rights.
5. Modified the request parameter from 'Admin=false' to 'Admin=true'.
6. Forwarded the modified request to the server.
7. The application treated the user as an administrator.
8. Accessed the admin functionality and deleted the user **carlos**.

## Payload / Parameter Used

### Original Request
Admin=false

### Modified Request
Admin=true

## Result
Successfully gained **administrator privileges** by modifying the request parameter and deleted the user **carlos**, which solved the lab.

## Impact
If user roles are controlled by client-side parameters, attackers can manipulate requests to escalate privileges. This can allow attackers to:

- Gain administrator access
- Modify or delete users
- Access sensitive data
- Perform unauthorized actions

## Mitigation
- Never trust client-side parameters for authorization decisions.
- Implement server-side access control checks.
- Use secure session-based role management.
- Validate user roles on the server before executing sensitive actions.

## Learning
Access control must always be enforced on the **server side**. If applications rely on request parameters to determine user roles, attackers can easily manipulate those parameters and gain unauthorized privileges.
