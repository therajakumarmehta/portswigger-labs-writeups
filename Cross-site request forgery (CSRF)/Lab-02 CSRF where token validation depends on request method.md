# Lab Name
CSRF where token validation depends on request method

## Vulnerability
Cross-Site Request Forgery (CSRF) – Method-Based Token Validation Bypass

## Objective
Exploit a CSRF vulnerability by changing the request method to bypass CSRF token validation and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the application validates the CSRF token only for POST requests

5. Change the request method from POST to GET

6. Remove the CSRF token parameter from the request

7. Send the modified request and verify that the email is updated successfully

8. Generate a CSRF PoC using the GET request

9. Upload the exploit to the Exploit Server

10. Deliver the exploit to the victim

11. When the victim visits the malicious page, the GET request is automatically sent and the email address is changed, solving the lab

## Payload Used

```html
<html>
  <body>
    <img src="https://0a0b00440446b91580961c1600e20098.web-security-academy.net/my-account/change-email?email=xyz@gmail.com.com">
  </body>
</html>
```

## Result
Successfully bypassed the CSRF protection by changing the request method and performed an unauthorized email change.

## Impact
- Unauthorized account modifications
- Account takeover opportunities
- User impersonation
- Sensitive information changes
- Circumvention of security controls

## Mitigation
- Validate CSRF tokens for all state-changing HTTP methods
- Do not rely on the request method for CSRF protection
- Validate Origin and Referer headers
- Use SameSite cookies
- Require server-side authorization checks for every sensitive request

## Learning
CSRF protection should be enforced consistently for every state-changing request.
Validating CSRF tokens only for specific HTTP methods allows attackers to bypass the protection simply by changing the request method.
