# Lab Name
Brute-forcing a stay-logged-in cookie

## Vulnerability
Authentication Vulnerability – Weak Cookie-based Authentication

## Objective
Brute-force Carlos's stay-logged-in cookie to access his account.

## Entry Point
Stay-logged-in cookie

## Exploitation Type
Cookie Brute-force / Weak Token Generation

## Methodology
1. Login using provided credentials:
   wiener:peter

2. Enable "Stay logged in" option and log in

3. Capture the login request from Burp Suite (HTTP history)

4. Send the request to Burp Intruder

5. Identify the stay-logged-in cookie

<img width="1742" height="811" alt="6 3" src="https://github.com/user-attachments/assets/ace01e77-e0b3-4a03-9b57-8725d255fff9" />

6. Modify the request:
   - Change username from wiener to carlos

7. Set payload position on the stay-logged-in cookie value

8. Configure payload:
   - Use candidate password list

9. Apply payload processing:
   - Add prefix: carlos:
   - Apply hash: MD5
   - Encode result in Base64

<img width="1882" height="860" alt="6 4" src="https://github.com/user-attachments/assets/acb67a2c-9f6f-4eed-928e-edfdcdd4c0be" />

10. Start the attack

11. Use "Grep Match" (e.g., "Update email") to identify successful response

12. Identify the correct cookie value from results

13. Copy the valid stay-logged-in cookie

<img width="1893" height="881" alt="6 6" src="https://github.com/user-attachments/assets/99d33eee-1c51-4ed4-8463-1efa5b3a2360" />

14. Go to browser storage (Application → Cookies)

15. Replace existing stay-logged-in cookie with the obtained value

<img width="1857" height="920" alt="6 7" src="https://github.com/user-attachments/assets/28de886f-6072-4cf3-a642-1d992a021cf2" />

16. Refresh the page

17. Access to carlos account is granted

## Payload Used

Format:
Base64( MD5( "carlos:password" ) )

## Result
Successfully brute-forced the stay-logged-in cookie and accessed the carlos account.

## Impact
- Unauthorized account access
- Weak session management
- Predictable authentication tokens
- Account takeover

## Mitigation
- Use strong, random, and unpredictable tokens
- Avoid storing sensitive data in cookies
- Implement secure session management
- Use proper encryption instead of weak hashing
- Invalidate tokens after logout

## Learning
Authentication tokens must be securely generated and protected.
Weak encoding and predictable logic can allow attackers to brute-force authentication cookies.
