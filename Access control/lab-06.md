## Lab Name
User ID controlled by request parameter with unpredictable user IDs

## Vulnerability
Access Control Vulnerability – Insecure Direct Object Reference (IDOR)

## Objective
Access the API key of carlos account by obtaining and using its unpredictable user ID.

## Entry Point
User profile access via user ID parameter

## Exploitation Type
Information Disclosure + Parameter Tampering

## Methodology
1. Login with provided user credentials
2. Observe that user IDs are not predictable like (353cd7d1-b41f-40ca-ad53-46546ea416ea)
3. Go to a blog post or any page with user interaction (e.g., comments)
4. Click on a username (e.g., carlos) to view their profile
5. Observe the URL:
   /user/profile?id=2708c19e-c59c-4e38-9977-5a52c964fc41

6. Copy the user ID of the target user (e.g., carlos)

7. Navigate to our own profile request

   Example:
   /my-account?id=353cd7d1-b41f-40ca-ad53-46546ea416ea

8. Replace our ID with the copied carlos ID

   /my-account?id=2708c19e-c59c-4e38-9977-5a52c964fc41
   
10. Load the request

11. Carlos account details are displayed

## Payload Used

Original:
id=<353cd7d1-b41f-40ca-ad53-46546ea416ea>

Modified:
id=<353cd7d1-b41f-40ca-ad53-46546ea416ea>

## Result
Successfully accessed the carlos account using its unpredictable user ID.

## Impact
- Unauthorized access to sensitive user data
- Bypass of access control mechanisms
- Potential account takeover

## Mitigation
- Enforce strict server-side authorization checks
- Do not rely on obscurity (unpredictable IDs) for security
- Validate that the requested resource belongs to the logged-in user
- Use proper access control mechanisms (RBAC)

## Learning
Unpredictable user IDs do not prevent IDOR vulnerabilities.
Proper authorization checks on the server side are required to secure user data.
