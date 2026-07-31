# Lab Name
SameSite Lax bypass via method override

## Vulnerability
Cross-Site Request Forgery (CSRF) – SameSite Lax Bypass via HTTP Method Override

## Objective
Exploit the application's HTTP method override functionality to bypass the SameSite=Lax restriction and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and change your email address.

3. Intercept the request using **Burp Suite Proxy** and locate the **POST /my-account/change-email** request in **HTTP History**.

4. Observe that the request does not contain any unpredictable CSRF token.

5. Inspect the response to the **POST /login** request and notice that the session cookie is issued without an explicit **SameSite** attribute, meaning the browser applies the default **SameSite=Lax** policy.

6. Send the **POST /my-account/change-email** request to **Burp Repeater**.

7. Right-click the request and select **Change request method** to convert it into a **GET** request.

8. Send the request and observe that the endpoint rejects GET requests.

9. Modify the request by adding the **_method=POST** parameter to the query string.

```http
GET /my-account/change-email?email=test@gmail.com&_method=POST HTTP/1.1
```

10. Send the modified request and observe that the server accepts it and updates the email address.

11. Open the **Exploit Server** and create the following exploit:

```html
<script>
document.location="https://0a42002804e8128481b30dc30018006b.web-security-academy.net/my-account/change-email?email=xyz@example.com&_method=POST";
</script>
```

12. Store the exploit and click **View exploit** to verify that your email address changes successfully.

13. Change the email address in the exploit so that it does not match your own.

14. Click **Deliver to victim**.

15. When the victim visits the exploit page, the browser performs a top-level **GET** navigation. Because of the default **SameSite=Lax** policy, the session cookie is included, while the **_method=POST** parameter causes the server to process the request as a POST request, changing the victim's email address and solving the lab.

## Payload Used

```html
<script>
document.location="https://0a42002804e8128481b30dc30018006b.web-security-academy.net/my-account/change-email?email=xyz@example.com&_method=POST";
</script>
```

## Result
Successfully bypassed the SameSite=Lax restriction using the HTTP method override feature and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of SameSite=Lax protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Disable unnecessary HTTP method override functionality.
- Enforce the expected HTTP method on the server.
- Implement unpredictable CSRF tokens.
- Explicitly configure cookies with appropriate SameSite attributes.
- Validate Origin and Referer headers for sensitive requests.

## Learning
SameSite=Lax cookies are included in top-level GET navigations. If an application supports HTTP method override using parameters such as **_method=POST**, an attacker can force the browser to send an authenticated GET request that the server interprets as a POST request, effectively bypassing the SameSite=Lax protection.
