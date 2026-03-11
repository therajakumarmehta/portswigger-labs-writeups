## Lab Name
Blind SQL Injection with Time Delays

## Vulnerability
SQL Injection – Blind (Time-Based)

## Objective
Confirm that the application is vulnerable to SQL injection by triggering a delay in the database response.

## Entry Point
TrackingId cookie

## Exploitation Type
Blind SQL Injection (Time Delay)

## Methodology

1. Intercepted the HTTP request using Burp Suite.
2. Observed that the application used the "TrackingId" cookie in a backend SQL query.
3. Inserted a single quote (') into the cookie value to test for SQL injection.
4. The application did not return any SQL error or visible response difference.
5. Tested for time-based SQL injection by injecting a database delay function.
6. Sent the modified request to the server and observed the response time.
7. The server response was delayed, confirming that the SQL query was executed by the database.

## Payload Used
TrackingId=xyz'||pg_sleep(10)--

## Result
The server response was delayed by 10 seconds, confirming that the injected SQL query was executed successfully and that the application is vulnerable to Blind SQL Injection.

## Impact
An attacker can use time-based SQL injection to extract sensitive information from the database even when error messages and query results are not visible.

## Mitigation

- Use parameterized queries (prepared statements).
- Validate and sanitize all user inputs including cookies.
- Implement proper error handling and avoid exposing database behavior to users.
- Apply Web Application Firewall (WAF) rules to detect SQL injection attempts.

## Learning
Blind SQL injection is used when applications do not display SQL errors or query results.

Attackers rely on indirect signals such as response time to determine whether the injected SQL query was executed.

By using database delay functions, attackers can confirm vulnerabilities and later extract sensitive data character by character.
