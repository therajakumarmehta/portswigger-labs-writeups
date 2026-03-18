## Lab Name
User ID controlled by request parameter with data leakage in redirect

## Vulnerability
Access Control Vulnerability – IDOR with Information Disclosure via Redirect

## Objective
Obtain the carlos API key by exploiting data leakage in a redirect.

## Entry Point
User account/profile endpoint with id parameter

## Exploitation Type
Parameter Tampering + Information Disclosure

## Methodology
1. Login with provided user credentials
2. Navigate to My Account page

   Example:
   /my-account?id=wiener

3. Intercept the request using Burp Suite

4. Modify the id parameter to carlos

   GET /my-account?id=carlos HTTP/1.1

5. Forward the request

6. Observe that access is denied but response contains a redirect (302)

7. Check the redirect response carefully (headers/body)

8. Sensitive data (such as API key) is leaked in the redirect response

9. Extract the carlos API key from the response

10. Submit the API key to complete the lab

## Payload Used

Original:
id=wiener

Modified:
id=carlos

## Result
Successfully obtained the carlos API key from the redirect response despite access restrictions.

## Impact
- Sensitive data leakage
- Bypass of access control
- Exposure of API keys or confidential information

## Mitigation
- Do not include sensitive data in redirect responses
- Implement strict server-side authorization checks
- Ensure proper handling of unauthorized requests
- Avoid leaking data in headers or response bodies

## Learning
Even when access is restricted, improper handling of redirects can leak sensitive data.
Always secure both responses and redirects to prevent information disclosure.
