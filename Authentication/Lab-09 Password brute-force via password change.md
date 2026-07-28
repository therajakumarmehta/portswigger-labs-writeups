# Lab Name
Password brute-force via password change

## Vulnerability
Authentication Vulnerability – Password Brute Force via Password Change Functionality

## Objective
Identify the victim's current password by abusing the password change functionality and log in as **carlos**.

## Entry Point
Change Password functionality

## Exploitation Type
Brute Force / Authentication Flaw

## Methodology
1. Open the lab and log in using the provided user credentials.

2. Navigate to the **Change Password** page.

3. Intercept the password change request using Burp Suite.

4. Send the request to Burp Suite Intruder.

5. Change the **username** parameter from your account to **carlos**.

6. Set the **Current Password** field as the Intruder payload position.

7. Intentionally enter two different values for **New Password** and **Confirm Password**.

8. Start the Intruder attack using a password wordlist.

9. Observe the server responses.

10. Most requests return an error indicating that the current password is incorrect.

11. When the correct current password is tested, the response changes to:

    **"New passwords do not match."**

12. This different response confirms the correct password for **carlos**.

13. Log in as **carlos** using the discovered password and complete the lab.

## Payload Used

Username:
carlos

Current Password:
§password§

New Password:
Password123

Confirm Password:
Password456

## Result
Successfully identified the correct password for **carlos** by detecting the **"New passwords do not match"** response and logged in to the victim's account, solving the lab.

## Impact
- User passwords can be brute-forced
- Unauthorized account access
- Account takeover
- Weak authentication security
- Information disclosure through different error messages

## Mitigation
- Return the same generic error message for all password change failures.
- Implement rate limiting and account lockout mechanisms.
- Require re-authentication for sensitive operations.
- Monitor and detect brute-force attempts.
- Enforce strong password policies.

## Learning
Applications should never reveal whether the current password is correct through different error messages. Consistent responses, rate limiting, and account lockout mechanisms are essential to prevent attackers from identifying valid passwords via brute-force attacks.
