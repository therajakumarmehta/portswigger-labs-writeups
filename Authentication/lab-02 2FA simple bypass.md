# Lab Name
2FA simple bypass

## Vulnerability
Authentication Vulnerability – Two-Factor Authentication Bypass

## Objective
Bypass the 2FA mechanism and access the victim (carlos) account.

## Entry Point
Login and 2FA verification process

## Exploitation Type
Authentication Bypass / Logic Flaw

## Methodology
1. Login using valid user credentials:
   wiener:peter

<img width="1851" height="918" alt="Screenshot 2026-03-21 220617" src="https://github.com/user-attachments/assets/9662a454-cc83-4790-aa09-d7c81292ff33" />

2. After login, a 2FA verification page is displayed

<img width="1845" height="920" alt="5 2" src="https://github.com/user-attachments/assets/51ee139f-89ee-410c-801f-ccce1c4a0457" />

3. Access the email client and retrieve the 2FA code

<img width="1852" height="912" alt="5 3" src="https://github.com/user-attachments/assets/b33ddd34-770f-459c-b111-b0089120e677" />

4. Enter the 2FA code and successfully log in to the wiener account

5. Navigate to the account page and observe the URL:

   /my-account?id=wiener

6. Copy this URL

<img width="1852" height="968" alt="4 5" src="https://github.com/user-attachments/assets/7c7f89a6-423a-4f76-8d1a-6a28574c1c9c" />

7. Logout from the current account

8. Login again using victim credentials (carlos)

9. After entering credentials, the application redirects to 2FA page:

   /login2

<img width="1867" height="981" alt="5 5" src="https://github.com/user-attachments/assets/a2758e8c-4ba3-4d58-9c81-b2bfebf7f467" />

10. Before completing 2FA, modify the URL:

   Replace:
   /login2

   With:
   /my-account?id=carlos

<img width="1861" height="972" alt="5 6" src="https://github.com/user-attachments/assets/72f96349-b857-4d69-b612-bdfc032aea3c" />

11. Load the modified URL

12. Observe that the carlos account is accessed without completing 2FA

## Payload Used

Original:
GET /login2

Modified:
GET /my-account?id=carlos

## Result
Successfully bypassed 2FA and accessed the carlos account without entering the verification code.

<img width="1851" height="910" alt="Screenshot 2026-03-21 221853" src="https://github.com/user-attachments/assets/a9278524-1c53-46ac-8529-9e49350f796f" />

## Impact
- Complete bypass of two-factor authentication
- Unauthorized access to user accounts
- High risk of account takeover
- Critical authentication flaw

## Mitigation
- Enforce 2FA validation on the server side
- Bind user session to successful 2FA verification
- Prevent direct access to authenticated endpoints before 2FA completion
- Validate authentication state on every request

## Learning
2FA must be strictly enforced on the backend.
If access is granted before completing 2FA, attackers can bypass it by manipulating URLs.
