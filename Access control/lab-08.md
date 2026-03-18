## Lab Name
User ID controlled by request parameter with password disclosure

## Vulnerability
Access Control Vulnerability – IDOR with Sensitive Data Exposure

## Objective
Retrieve the administrator password and log in as administrator and delete carlos user.

## Entry Point
User account/profile endpoint with id parameter

## Exploitation Type
Parameter Tampering / IDOR

## Methodology
1. Login with provided user credentials
2. Navigate to My Account page

   Example:
   /my-account?id=wiener

3. Intercept the request using Burp Suite

4. Modify the id parameter to administrator

   GET /my-account?id=administrator HTTP/1.1

5. Forward the request

6. Observe that administrator account details are returned

7. Locate the password field in the response

8. Copy the administrator password

9. Logout from current account

10. Login as administrator using the obtained password
11. Go to the admin pannel and delete carlos user

## Payload Used

Original:
id=wiener

Modified:
id=administrator

## Result
Successfully retrieved the administrator password and logged in as administrator and delete carlos user.

## Impact
- Exposure of user passwords
- Unauthorized account access
- Full account takeover
- Critical data breach

## Mitigation
- Never expose passwords in responses (use hashing)
- Implement strict server-side authorization checks
- Do not allow access to other users’ data via parameters
- Follow secure data handling practices

## Learning
Sensitive data like passwords should never be returned in responses.
Proper access control and secure storage (hashing) are essential to prevent such vulnerabilities.
