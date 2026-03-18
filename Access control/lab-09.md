## Lab Name
Insecure Direct Object References

## Vulnerability
Access Control Vulnerability – Insecure Direct Object Reference (IDOR)

## Objective
Find the password for the user carlos from chat logs and log in to their account.

## Entry Point
Static file URLs used to access chat logs

## Exploitation Type
Direct Object Reference / File Path Manipulation

## Methodology
1. Login with provided user credentials

2. Navigate to the chat functionality

3. Send a message and observe that chat logs are stored on the server

4. Identify that chat logs are accessed via static URLs

   Example:
    /download-transcript/1.txt

5. Intercept or observe the request for chat log files

6. Modify the file name or ID in the URL to access other users' chat logs

   Example:
   /download-transcript/1.txt
   /download-transcript/1.txt

7. Iterate through different file IDs to locate other users' chat logs

8. Find the chat log belonging to user carlos

9. Extract the password from the chat log

10. Logout from the current account

11. Login as carlos using the obtained password

## Payload Used

Original:
GET /download-transcript/2.txt

Modified:
GET /download-transcript/1.txt

## Result
Successfully accessed chat logs via direct object reference, retrieved carlos's password, and logged into their account.

## Impact
- Unauthorized access to sensitive files
- Exposure of user credentials
- Privacy violation
- Account takeover

## Mitigation
- Implement strict access control for file access
- Avoid exposing direct file paths
- Use randomized or indirect references
- Validate user authorization before serving files

## Learning
Direct access to internal files without proper authorization leads to IDOR vulnerabilities.
Sensitive data should never be exposed through predictable or accessible file paths.
