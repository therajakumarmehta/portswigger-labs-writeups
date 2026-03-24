# Lab Name
Password reset poisoning via middleware

## Vulnerability
Authentication Vulnerability – Password Reset Poisoning

## Objective
Gain access to Carlos's account by poisoning the password reset link.

## Entry Point
Forgot password functionality

## Exploitation Type
Header Injection / Host Header Poisoning

## Methodology
1. Login using provided credentials:
   wiener:peter

2. Click on "Forgot Password" and submit request for user:
   wiener

3. Intercept the password reset request and send it to Repeater

4. Modify the request:
   - Change username from wiener to carlos
   - Add header:
     X-Forwarded-Host: <exploit-server-url>

5. Send the modified request

6. The application sends a password reset link to carlos containing the poisoned host

7. Go to the exploit server and check incoming requests/logs

8. Capture the password reset token from the request made by carlos

9. Now perform a normal password reset for wiener and intercept the request

10. Replace the reset token in the request with the stolen token of carlos

11. Set a new password and send the request

12. Password for carlos is successfully changed

13. Login using:
   username: carlos
   password: (new password)

## Payload Used

Header:
X-Forwarded-Host: <exploit-server-url>

## Result
Successfully poisoned the password reset link, captured Carlos's reset token, and reset his password to gain account access.

## Impact
- Unauthorized password reset
- Full account takeover
- Sensitive token leakage
- Critical authentication vulnerability

## Mitigation
- Do not trust user-controlled headers like X-Forwarded-Host
- Validate and sanitize host headers
- Generate absolute URLs securely on the server side
- Bind reset tokens to specific users and sessions
- Expire tokens after single use

## Learning
Improper handling of host headers can lead to password reset poisoning.
Applications must validate all user-controlled inputs, including headers, to prevent account takeover.
