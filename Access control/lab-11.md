## Lab Name
Method-based access control can be circumvented

## Vulnerability
Access Control Vulnerability – Broken Access Control (HTTP Method Bypass)

## Objective
Promote yourself to administrator by bypassing method-based access control.

## Entry Point
Admin functionality restricted based on HTTP methods

## Exploitation Type
HTTP Method Manipulation / Access Control Bypass

## Methodology
1. Login using normal user credentials:
   wiener:peter

2. Observe available functionalities and requests

3. Try accessing admin functionality (restricted)

4. Intercept request using Burp Suite

5. Identify a request where method-based restriction is applied (e.g., POST blocked)

6. Change the HTTP method (e.g., POST → GET or GET → POST)

   Example:
   POST /admin-roles HTTP/1.1

   Change to:
   GET /admin-roles HTTP/1.1

7. Forward the modified request

8. Observe that access control is bypassed

9. Modify parameters to promote user role

10. Send request and gain administrator privileges

## Payload Used

Original:
POST /admin-roles

Modified:
GET /admin-roles

## Result
Successfully bypassed method-based access control and gained administrator privileges.

## Impact
- Unauthorized access to restricted functionality
- Privilege escalation
- Ability to perform admin actions
- Full application compromise

## Mitigation
- Do not rely on HTTP methods for access control
- Implement strict server-side authorization checks
- Validate user roles for every request
- Ensure consistent access control across all HTTP methods

## Learning
Access control should not depend on HTTP methods alone.
Proper authorization checks must be enforced regardless of request method.
