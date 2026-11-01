# Lab Name
Password reset broken logic

## Vulnerability
Authentication Vulnerability – Broken Password Reset Logic

## Objective
Reset the password of user carlos and log in to their account.

## Entry Point
Forgot password functionality

## Exploitation Type
Parameter Tampering / Logic Flaw

## Methodology
1. Click on "Forgot Password" option

2. Enter username:
   wiener

3. Open the email client and receive the password reset link

4. Click on the reset link

5. A "Set new password" page is displayed

6. Intercept the request using Burp Suite

7. Observe parameters in the request:
   - username=wiener
   - reset token (temporary token)

<img width="1806" height="802" alt="6 1" src="https://github.com/user-attachments/assets/832a8865-76d0-4cdc-95a8-38ea50ca3db2" />

8. Modify the request:
   - Change username from wiener to carlos
   - Remove or manipulate the reset token parameter

<img width="1597" height="747" alt="6 2" src="https://github.com/user-attachments/assets/2f4c8c27-dc0a-4de6-b987-43dea535c62b" />

9. Send the modified request

10. Observe response (302 redirect), indicating password reset success

<img width="1885" height="789" alt="Screenshot 2026-03-22 122302" src="https://github.com/user-attachments/assets/55aee399-2e0b-41f6-b97f-862939d598d1" />

11. Login using:
   username: carlos
   password: (new password set)

## Payload Used

Original:
username=wiener
token=<valid_token>

Modified:
username=carlos
token= (removed/modified)

## Result
Successfully reset the password of user carlos and logged into the account.

<img width="1838" height="920" alt="image" src="https://github.com/user-attachments/assets/f8ead95d-7941-4d89-9896-d5e6cff28fa2" />

## Impact
- Unauthorized password reset
- Full account takeover
- Critical authentication bypass
- Exposure of user accounts

## Mitigation
- Bind reset tokens to specific users
- Validate reset token on server side
- Do not allow modification of username in reset requests
- Expire tokens after single use
- Implement strong verification for password reset

## Learning
Password reset functionality must securely validate tokens and user identity.
Improper validation can allow attackers to reset passwords of other users.
