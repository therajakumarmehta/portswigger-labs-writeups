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

## Result
 Identified the database type and version of Oracle..

## Learning
- UNION-based SQL injection can be used to identify the backend database when query output is reflected.
- The correct number of columns must be identified before using UNION SELECT, otherwise the query fails.
- NULL values are used as placeholders when the data type of other columns is unknown.
- Oracle databases expose version and banner information through the v$version system table.
- The BANNER column in v$version reveals database type and version details.
- Extracting database version helps attackers choose database-specific payloads for further exploitation.
- Improper input validation allows attackers to query sensitive system tables.
