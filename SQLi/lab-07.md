# Lab Name
SQL injection attack, querying the database type and version on MySQL and Microsoft

## Vulnerability
SQL Injection (UNION-based)

## Objective
Exploit UNION-based SQL Injection to querying the database type and version on MySQL and Microsoft

## Entry Point
Category parameter

## Payload Used
  UNION SELECT NULL, @@version#

## Result
Identified the database type and version using @@version indicating  MySQL/Microsoft SQL Server.

## Learning
- UNION-based SQL injection can be used to identify the backend database when query output is reflected.
- The correct number of columns must be identified before using UNION SELECT, otherwise the query fails.
- NULL values are used as placeholders when the data type of other columns is unknown.
- MySQL and Microsoft databases expose version and type of database information through the @@version system table.
- Extracting database version helps attackers choose database-specific payloads for further exploitation.
- Improper input validation allows attackers to query sensitive system tables.

