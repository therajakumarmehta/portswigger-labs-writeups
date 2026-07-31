# Lab Name
SameSite Strict bypass via client-side redirect

## Vulnerability
Cross-Site Request Forgery (CSRF) – SameSite Strict Bypass via Client-Side Redirect

## Objective
Bypass the SameSite=Strict cookie restriction by abusing a client-side redirect gadget and change the victim's email address.

## Entry Point
Comment confirmation page and Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and change your email address.

3. In **Burp Suite**, go to **Proxy > HTTP History** and inspect the **POST /my-account/change-email** request.

4. Observe that the request does not contain any unpredictable CSRF token.

5. Inspect the response to the **POST /login** request and notice that the session cookie is set with the **SameSite=Strict** attribute.

6. Navigate to any blog post and submit a comment.

7. Observe that after submitting the comment, you are redirected to:

```text
/post/comment/confirmation?postId=x
```

8. In **Burp HTTP History**, identify that the redirect is handled by the JavaScript file:

```text
/resources/js/commentConfirmationRedirect.js
```

9. Inspect the JavaScript and observe that it uses the **postId** parameter to dynamically construct the redirect URL.

10. Copy the confirmation page URL and replace the **postId** value with any string:

```text
/post/comment/confirmation?postId=foo
```

11. Observe that the application attempts to redirect to:

```text
/post/foo
```

12. Replace the **postId** value with a path traversal payload:

```text
/post/comment/confirmation?postId=1/../../my-account
```

13. Observe that the browser normalizes the path and redirects you to the **My Account** page, confirming that the client-side redirect can be abused to access arbitrary endpoints on the target site.

14. Open the **Exploit Server** and create the following exploit:

```html
<script>
document.location="https://0a7e006e0415b777803cb8f900a800ea.web-security-academy.net/post/comment/confirmation?postId=../my-account";
</script>
```

15. Store the exploit and click **View exploit**.

16. Observe that the client-side redirect takes you to the **My Account** page while keeping you authenticated, confirming that the browser includes the **SameSite=Strict** session cookie during the same-site redirect.

17. Send the **POST /my-account/change-email** request to **Burp Repeater**.

18. Right-click the request and select **Change request method** to generate the equivalent **GET** request.

19. Send the request and observe that the endpoint accepts the **GET** request and successfully changes the email address.

20. Update the exploit as follows:

```html
<script>
document.location="https://0a7e006e0415b777803cb8f900a800ea.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=xyz@example.com%26submit=1";
</script>
```

21. Store the exploit and click **View exploit** to verify that your email address changes successfully.

22. Replace the email address with an attacker-controlled email address.

23. Click **Deliver to victim**.

24. When the victim visits the exploit page, the browser first makes a cross-site request to the comment confirmation page. The vulnerable client-side JavaScript then performs a same-site redirect to the email change endpoint, causing the **SameSite=Strict** session cookie to be included. The victim's email address is changed successfully, solving the lab.

## Payload Used

```html
<script>
document.location="https://0a7e006e0415b777803cb8f900a800ea.web-security-academy.net/post/comment/confirmation?postId=1/../../my-account/change-email?email=xyz@example.com%26submit=1";
</script>
```

## Result
Successfully bypassed the **SameSite=Strict** protection by exploiting a client-side redirect gadget and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of SameSite=Strict protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Do not rely solely on SameSite cookies for CSRF protection.
- Validate and sanitize client-side redirect parameters.
- Prevent path traversal in redirect logic.
- Implement unpredictable CSRF tokens.
- Validate Origin and Referer headers for state-changing requests.

## Learning
Although **SameSite=Strict** cookies are not included in cross-site requests, they are included in subsequent same-site requests triggered by client-side redirects. If an application contains a client-side redirect gadget that can be manipulated using user-controlled input, an attacker can exploit it to bypass SameSite=Strict protections and perform CSRF attacks.
