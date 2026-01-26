# Lab Name
SQL injection UNION attack, retrieving data from other tables

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to retrieving data from other tables

## Entry Point
Category parameter

## Payload Used
  UNION SELECT username, password FROM users--

## Result
Identified all username and their password from other table.

## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
Final UNION query extract data.
