# Lab Name
CSRF with broken Referer validation

## Vulnerability
Cross-Site Request Forgery (CSRF) – Broken Referer Validation

## Objective
Exploit the application's flawed Referer validation to bypass the CSRF protection and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and submit the **Update email** form.

3. In **Burp Suite**, locate the **POST /my-account/change-email** request in **Proxy > HTTP History**.

4. Send the request to **Burp Repeater**.

5. Modify the **Referer** header by replacing the original domain with an arbitrary domain and send the request.

6. Observe that the server rejects the request because the Referer header no longer contains the expected domain.

7. Copy the original domain of your lab instance and append it to the arbitrary domain as a query string.

Example:

```http
Referer: https://xyz.com?0a9f001703c455dd80ae03ac008100ec.web-security-academy.net
```

8. Send the modified request again.

9. Observe that the request is accepted, indicating that the application only checks whether the expected domain appears anywhere within the Referer header instead of validating its actual origin.

10. Open the **Exploit Server** and generate a CSRF proof of concept from the email change request.

11. Modify the generated JavaScript by updating the third parameter of the **history.pushState()** function as follows:

```javascript
history.pushState("", "", "/?0a9f001703c455dd80ae03ac008100ec.web-security-academy.net")
```

12. This causes the browser to include the target application's URL inside the query string of the Referer header, allowing it to satisfy the application's weak validation.

13. In the **Exploit Server**, add the following header to the **Head** section:

```http
Referrer-Policy: unsafe-url
```

14. This ensures that the browser includes the complete URL, including the query string, in the Referer header instead of stripping it.

15. Modify the email address in the exploit so that it points to an attacker-controlled email address.

16. Store the exploit and click **View exploit** to verify that the request is accepted.

17. Click **Deliver to victim**.

18. When the victim visits the exploit page, the browser sends a Referer header containing the target domain inside the query string. Because the application only checks for the presence of the expected domain anywhere in the Referer header, the CSRF request is accepted and the victim's email address is changed successfully, solving the lab.

## Payload Used

### Referer Header

```http
Referer: https://xyz.com?0a9f001703c455dd80ae03ac008100ec.web-security-academy.net
```

### JavaScript

```javascript
history.pushState("", "", "/?0a9f001703c455dd80ae03ac008100ec.web-security-academy.net")
```

### Exploit Server Header

```http
Referrer-Policy: unsafe-url
```
```html
<html>
  <body>
    <form action="https://0a9f001703c455dd80ae03ac008100ec.web-security-academy.net/my-account/change-email" method="POST">
      <input type="hidden" name="email" value="xyz@example.com">
    </form>

    <script>
      history.pushState("", "", "/?0a9f001703c455dd80ae03ac008100ec.web-security-academy.net");
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the application's broken Referer validation and changed the victim's email address by crafting a Referer header that contained the expected domain within its query string.

## Impact
- Unauthorized account modifications
- Bypass of Referer-based CSRF protection
- User impersonation
- Account takeover opportunities
- Unauthorized execution of sensitive actions

## Mitigation
- Never validate the Referer header using substring matching.
- Verify that the Referer or Origin header exactly matches the expected trusted origin.
- Implement unpredictable CSRF tokens for all state-changing requests.
- Use SameSite cookies as an additional layer of defense.
- Perform strict server-side validation before processing sensitive requests.

## Learning
This vulnerability exists because the application performs an insecure Referer validation by checking only whether the expected domain appears anywhere within the header. By placing the legitimate domain inside the query string of an attacker-controlled URL and forcing the browser to include the full Referer using **Referrer-Policy: unsafe-url**, an attacker can bypass the Referer validation and perform a successful CSRF attack.
