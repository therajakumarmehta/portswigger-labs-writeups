# Lab Name
SQL injection attack, querying the database type and version on MySQL and Microsoft

<img width="1843" height="913" alt="Screenshot 2026-05-01 003151" src="https://github.com/user-attachments/assets/1475a507-0d7f-4021-80d7-c69f6e03f617" />

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to querying the database type and version on MySQL and Microsoft

## Entry Point
Category parameter

## Payload Used
  UNION SELECT NULL, @@version#

  <img width="1505" height="793" alt="1 2" src="https://github.com/user-attachments/assets/54dc1cf3-99ae-41ca-b42c-ea70ee473946" />


## Result
Identified the database type and version using @@version indicating  MySQL/Microsoft SQL Server.

<img width="1507" height="786" alt="1 3" src="https://github.com/user-attachments/assets/80daccf7-be9e-47fd-a17b-882be12abb00" />


## Learning
- UNION-based SQL injection can be used to identify the backend database when query output is reflected.
- The correct number of columns must be identified before using UNION SELECT, otherwise the query fails.
- NULL values are used as placeholders when the data type of other columns is unknown.
- MySQL and Microsoft databases expose version and type of database information through the @@version system table.
- Extracting database version helps attackers choose database-specific payloads for further exploitation.
- Improper input validation allows attackers to query sensitive system tables.

