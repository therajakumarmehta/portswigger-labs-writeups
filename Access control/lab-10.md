## Lab Name
URL-based access control can be circumvented

## Vulnerability
Access Control Vulnerability – Broken Access Control (URL-based bypass)

## Objective
Access the admin panel and delete the user carlos.

## Entry Point
/admin endpoint (blocked by front-end control)

## Exploitation Type
Header Manipulation / Access Control Bypass

## Methodology
1. Open the lab and observe that /admin endpoint exists but is blocked

2. Try accessing:
   /admin
   → Access denied

3. Intercept the request using Burp Suite

4. Modify the request by adding the following header:

   X-Original-URL: /admin

5. Send the request to the server

6. Observe that the admin panel is accessible

7. Locate the option to delete users

8. Send another request to delete user carlos

   Add header again if required:
   X-Original-URL: /admin/delete?username=carlos

9. Forward the request

10. User carlos is successfully deleted

## Payload Used

Header:
X-Original-URL: /admin

For deletion:
X-Original-URL: /admin/delete?username=carlos

## Result
Successfully bypassed URL-based access control using the X-Original-URL header and deleted the user carlos.

## Impact
- Unauthorized access to admin panel
- Privilege escalation
- Ability to perform administrative actions
- Full application compromise

## Mitigation
- Do not rely on front-end access control
- Enforce access control checks on the server side
- Properly validate and restrict special headers
- Disable or securely handle headers like X-Original-URL

## Learning
Front-end restrictions can be bypassed easily.
Access control must always be enforced on the back-end server.
