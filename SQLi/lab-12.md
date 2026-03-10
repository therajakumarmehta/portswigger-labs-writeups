# Lab Name
Visible error-based SQL injection

## Vulnerability
SQL Injection – Error-based information disclosuer

## Objective
Log in as the administrator user.

## Entry Point
TrackingId cookie

## Exploitation Type
Visible Error-Based SQL Injection

## Methodology
1. Intercepted the request using a proxy tool.
2. Observed that the application used the TrackingId cookie in a backend SQL query.
3. Inserted a single quote (') into the cookie value to test for SQL injection.
4. The application returned a SQL error message, confirming the vulnerability.
5. Crafted an error-based payload that forced the database to return query results within the error message.
6. Extracted the administrator password from the database.
7. Used the extracted credentials to log in as the administrator.

## Payload Used
TrackingId=' AND CAST((SELECT password FROM users LIMIT 1) AS int)--

## Result
Successfully extracted the administrator password from the database and logged in as the administrator account.

## Impact
An attacker can retrieve sensitive data such as usernames and passwords directly from the database through visible error messages.

## Mitigation
- Use parameterized queries (prepared statements).
- Properly validate and sanitize all user inputs, including cookies.
- Disable detailed SQL error messages in production environments.

## Learning
Error-based SQL injection allows attackers to extract sensitive information by forcing the database to generate error messages containing query results.  
Applications should never expose database errors to users and should use secure query handling techniques.
