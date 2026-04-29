# Lab Name
SQL injection attack, querying the database type and version on Oracle.

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to querying the database type and version on Oracle.

## Entry Point
Category parameter

## Payload Used
  UNION SELECT BANNER, NULL FROM v$version--
  
  <img width="1492" height="828" alt="Screenshot 2026-04-29 132159" src="https://github.com/user-attachments/assets/71bb565f-6f7f-441e-9a77-a63ff9dd31bb" />


## Result
 Identified the database type and version of Oracle..
 
 <img width="1875" height="887" alt="Screenshot 2026-04-29 132321" src="https://github.com/user-attachments/assets/890d90e9-d4c5-46b0-90ad-33256947e139" />


## Learning
- UNION-based SQL injection can be used to identify the backend database when query output is reflected.
- The correct number of columns must be identified before using UNION SELECT, otherwise the query fails.
- NULL values are used as placeholders when the data type of other columns is unknown.
- Oracle databases expose version and banner information through the v$version system table.
- The BANNER column in v$version reveals database type and version details.
- Extracting database version helps attackers choose database-specific payloads for further exploitation.
- Improper input validation allows attackers to query sensitive system tables.
