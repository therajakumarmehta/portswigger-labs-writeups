# Lab Name
SQL injection UNION attack, retrieving multiple values in a single column

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to retrieving multiple values in a single column

## Entry Point
Category parameter

## Payload Used
  UNION SELECT NULL, username ||'~'|| password FROM users--

## Result
Identified all username and their password from multiple values in a single column.

## Impact
Attacker can extract sensitive user credentials from the database.

## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
String concatenation ( || ) can be used to merge values into a single column and '~' is used to seperate two values.
Final UNION query extract data.
