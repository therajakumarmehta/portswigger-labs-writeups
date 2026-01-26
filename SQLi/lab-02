# Lab Name
SQL injection UNION attack, determining the number of columns returned by the query

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to determine the number of columns returned by the query.

## Entry Point
Category parameter

## Payload Used
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
' UNION SELECT NULL, NULL, NULL--

## Result
Identified that the query returns 3 columns.

## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
