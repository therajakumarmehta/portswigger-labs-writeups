# Lab Name
CSRF where Referer validation depends on header being present

## Vulnerability
Cross-Site Request Forgery (CSRF) – Referer Header Validation Bypass

## Objective
Bypass the application's Referer-based CSRF protection and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and submit the **Update email** form.

3. In **Burp Suite**, locate the **POST /my-account/change-email** request in **Proxy > HTTP History**.

4. Send the request to **Burp Repeater**.

5. Modify the **Referer** header by changing its domain to any arbitrary value and send the request.

6. Observe that the server rejects the request because the **Referer** header no longer contains the expected domain.

7. Delete the **Referer** header completely and resend the request.

8. Observe that the server accepts the request even though the **Referer** header is missing, indicating that the application validates the header only when it is present.

9. Open the **Exploit Server** and generate a CSRF proof of concept based on the email change request.

10. Add the following meta tag inside the `<head>` section of the exploit to suppress the **Referer** header:

```html
<meta name="referrer" content="no-referrer">
```

11. Modify the email address in the exploit so that it points to an attacker-controlled email address.

12. Store the exploit and click **View exploit** to verify that the request executes successfully.

13. Click **Deliver to victim**.

14. When the victim visits the exploit page, the browser omits the **Referer** header due to the meta tag. Since the application only validates the Referer when it is present, the request is accepted and the victim's email address is changed, solving the lab.

## Payload Used

```html
<html>
<head>
  <meta name="referrer" content="no-referrer">
</head>
  <body>
    <form action="https://0a14001c04cc5c81813dcfcd002d00af.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xxyz&#64;gmail&#46;com" />
    </form>
    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the application's Referer-based CSRF protection by suppressing the **Referer** header and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of Referer-based CSRF protection
- User impersonation
- Account takeover opportunities
- Unauthorized execution of sensitive actions

## Mitigation
- Do not rely solely on the **Referer** header for CSRF protection.
- Reject requests when the **Referer** or **Origin** header is missing or invalid.
- Implement unpredictable CSRF tokens for all state-changing requests.
- Validate the authenticated user's session before processing sensitive operations.
- Use **SameSite** cookies as an additional layer of defense rather than the primary protection mechanism.

## Learning
This vulnerability occurs because the application validates the **Referer** header only when it is present. By suppressing the header using the **`<meta name="referrer" content="no-referrer">`** tag, an attacker can force the browser to omit the Referer completely. Since the server accepts requests with a missing Referer header, the CSRF protection can be bypassed, allowing unauthorized actions to be performed on behalf of the victim.
