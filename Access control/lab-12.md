## Lab Name
Multi-step process with no access control on one step

## Vulnerability
Access Control Vulnerability – Broken Access Control in Multi-step Process

## Objective
Promote ourself to administrator by exploiting missing access control in one step.

## Entry Point
Admin role change functionality (multi-step process)

## Exploitation Type
Access Control Bypass / Parameter Manipulation

## Methodology
1. Login using normal user credentials:
   wiener:peter

2. Observe that changing user roles involves multiple steps

3. Login as administrator (for understanding flow):
   administrator:admin

4. Navigate to admin panel and observe role change process

5. Intercept the role change request using Burp Suite

6. Identify multiple steps in the request flow

7. Notice that one step does not enforce proper access control

8. Logout from admin account and login again as normal user

9. Directly access or replay the vulnerable step request

10. Modify parameters to promote your user to administrator

11. Forward the request

12. Your account is successfully upgraded to admin

## Payload Used

Example:
POST /admin-roles HTTP/1.1
username=wiener&role=administrator

## Result
Successfully bypassed access control in a multi-step process and gained administrator privileges.

## Impact
- Privilege escalation
- Unauthorized access to admin functionality
- Ability to modify user roles
- Full application compromise

## Mitigation
- Enforce access control checks at every step of the process
- Do not assume earlier steps guarantee security
- Validate user permissions for each request
- Implement proper role-based access control (RBAC)

## Learning
Each step in a multi-step process must have proper authorization checks.
Missing validation in any step can lead to privilege escalation.
