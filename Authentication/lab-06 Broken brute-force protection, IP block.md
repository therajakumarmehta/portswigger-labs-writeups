## Lab Name
Broken brute-force protection, IP block

## Vulnerability
Authentication Vulnerability – Broken Brute-force Protection

## Objective
Brute-force the password of user carlos and log in to their account.

## Entry Point
Login functionality

## Exploitation Type
Brute-force Attack / Logic Flaw Bypass

## Methodology
1. Login with provided credentials:
   wiener:peter

2. Observe login functionality and brute-force protection

3. Attempt multiple login requests for user carlos

4. Notice that after several failed attempts, IP gets blocked

<img width="1832" height="908" alt="4 1" src="https://github.com/user-attachments/assets/c664400f-7808-4911-be54-624c4cc90328" />


5. Intercept login requests using Burp Suite

6. Use Burp Intruder to perform brute-force attack

7. Configure attack:
   - Username: carlos
   - Password list: provided candidate passwords

8. To bypass IP blocking:
   - Alternate login attempts with valid login (wiener:peter)

<img width="1907" height="861" alt="4 2" src="https://github.com/user-attachments/assets/7658e218-2ca5-4bf0-a231-c3c6c3986f3e" />

<img width="1912" height="883" alt="4 3" src="https://github.com/user-attachments/assets/6505962a-42b4-4f2f-b143-dc1c2dbf6f4c" />

   - Or reset failed attempt counter by sending valid requests

10. Continue brute-force attack

11. Identify correct password based on successful response

<img width="1885" height="901" alt="4 4" src="https://github.com/user-attachments/assets/697b990c-3fa6-4a02-84c8-4baa4273d71e" />

12. Login as carlos using the discovered password

## Payload Used

Username:
carlos

Passwords:
(list of candidate passwords)

## Result
Successfully bypassed brute-force protection, identified the correct password, and logged in as user carlos.

<img width="1858" height="920" alt="image" src="https://github.com/user-attachments/assets/eb08af88-d011-4a95-ad05-62dc46c2d0ea" />

## Impact
- Account compromise
- Unauthorized access
- Weak authentication security
- Increased risk of credential attacks

## Mitigation
- Implement proper rate limiting
- Use account lockout mechanisms
- Apply CAPTCHA after failed attempts
- Monitor and block suspicious activity
- Enforce strong password policies

## Learning
Brute-force protection must be properly implemented.
Logic flaws in protection mechanisms can allow attackers to bypass restrictions and compromise accounts.
