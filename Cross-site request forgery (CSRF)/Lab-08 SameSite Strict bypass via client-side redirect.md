# Lab Name
SameSite Strict bypass via client-side redirect

## Vulnerability
Cross-Site Request Forgery (CSRF) – SameSite Strict Bypass via Client-Side Redirect

## Objective
Exploit a CSRF vulnerability by bypassing the SameSite=Strict cookie restriction using a client-side redirect and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Identify an open redirect or client-side redirect functionality within the application

4. Intercept the email change request using Burp Suite

5. Verify that the change-email endpoint requires authentication and is protected by SameSite=Strict cookies

6. Craft an exploit that first redirects the victim to the vulnerable client-side redirect endpoint

7. Configure the redirect to automatically navigate to the change-email endpoint with the required parameters

8. Upload the exploit to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the exploit page, the client-side redirect causes the browser to make a same-site request, allowing the SameSite=Strict cookie to be included

11. Observe that the victim's email address is changed successfully, solving the lab

## Payload Used

```html
<script>
location="https://0ab100c704bd910b80790387004d00af.web-security-academy.net/post/comment/confirmation?postId=1&redirect=/my-account/change-email?email=xyz@gmail.com%26submit=1";
</script>
```

## Result
Successfully bypassed the SameSite=Strict protection using a client-side redirect and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of SameSite=Strict protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Do not rely solely on SameSite cookies for CSRF protection
- Validate and restrict client-side redirects
- Implement server-side CSRF token validation
- Validate Origin and Referer headers
- Avoid open or unsafe redirect mechanisms

## Learning
SameSite=Strict cookies provide strong protection against cross-site requests, but they can be bypassed if an application performs unsafe client-side redirects. Sensitive actions should always be protected with server-side CSRF validation in addition to browser security mechanisms.
