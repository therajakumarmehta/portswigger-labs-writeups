## Lab Name
Blind SQL injection with time delays and information retrieval

## Vulnerability
SQL Injection – Blind SQL Injection (Time Delay)

## Objective
Retrieve the password for the administrator user.

## Entry Point
TrackingId cookie

## Exploitation Type
Blind SQL Injection using time delays

## Methodology
1. Intercepted the request using a proxy tool.
2. Observed that the TrackingId cookie was used in a backend SQL query.
3. Since no error messages were displayed, tested for blind SQL injection using a time delay function.
4. Injected a payload that caused a delay in the response.
5. The delayed response confirmed that the SQL query was being executed.
6. Used conditional queries to check database values.
7. Extracted the administrator password character by character using the time delay technique.

## Payload Used

Confirm SQL injection

TrackingId=x'||pg_sleep(5)--

Extract password characters

TrackingId=x'|| SELECT CASE WHEN (SUBSTRING(password,1,1)='a') THEN pg_sleep(5) ELSE pg_sleep(0) END FROM users WHERE username='administrator'--

## Result
Successfully extracted the password of the administrator account using time-based blind SQL injection.

## Impact
An attacker can extract sensitive data such as passwords from the database even when no error messages or output are displayed.

## Mitigation
- Use parameterized queries (prepared statements).
- Validate and sanitize all user inputs including cookies.
- Implement proper error handling and avoid exposing database behavior.
- Use Web Application Firewalls (WAF) to detect SQL injection attempts.

## Learning
Blind SQL injection can still allow attackers to retrieve sensitive information by observing differences in response time. 

Even without visible errors, attackers can exploit database queries to extract data.
