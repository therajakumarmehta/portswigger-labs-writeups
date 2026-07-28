# Lab Name
Referer-based access control

## Vulnerability
Access Control Vulnerability – Referer-Based Authorization Bypass

## Objective
Bypass the application's Referer-based access control and delete the user **carlos**.

## Entry Point
Admin functionality protected by the Referer header

## Exploitation Type
Access Control Bypass

## Methodology
1. Open the lab and log in using the provided user credentials.

2. Browse the application and identify an endpoint that performs an administrative action.

3. Intercept the request using Burp Suite.

4. Observe that access to the endpoint is controlled by checking the **Referer** header.

5. Notice that removing or modifying the Referer header affects the authorization decision.

6. Add or modify the Referer header so that it contains the expected administrative URL.

7. Forward the modified request.

8. Observe that the server accepts the request because it trusts the Referer header.

9. Access the admin functionality and delete the user **carlos**.

## Payload Used

```
Referer: https://0aaf00570412364e8095ee27000b0013.web-security-academy.net/admin
```

## Result
Successfully bypassed the Referer-based access control by supplying a trusted Referer header and deleted the user **carlos**, solving the lab.

## Impact
- Unauthorized access to administrative functionality
- Privilege escalation
- Unauthorized modification or deletion of user accounts
- Exposure of sensitive data
- Complete compromise of access control

## Mitigation
- Never rely on the Referer header for authorization decisions.
- Enforce server-side access control based on authenticated user roles.
- Validate user permissions for every sensitive request.
- Follow the principle of least privilege.
- Log and monitor unauthorized access attempts.

## Learning
The Referer header is completely controlled by the client and should never be used to enforce access control. Authorization decisions must always be performed on the server using the authenticated user's permissions rather than relying on client-supplied headers.
