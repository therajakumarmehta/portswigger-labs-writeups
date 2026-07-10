# Lab Name
Reflected XSS into a template literal with angle brackets, single, double quotes, backslash and backticks Unicode-escaped

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Exploit a reflected XSS vulnerability by injecting JavaScript into a template literal despite multiple character encodings.

## Entry Point
Search functionality

## Exploitation Type
Reflected XSS / JavaScript Template Literal Injection

## Methodology
1. Open the lab and locate the search functionality

2. Submit a normal search request

3. Observe that the search term is reflected inside a JavaScript template literal

4. Notice that:
   - Angle brackets (< and >) are HTML-encoded
   - Single quotes (') are escaped
   - Double quotes (") are HTML-encoded
   - Backslashes (\) are escaped
   - Backticks (`) are Unicode-escaped

5. Since the input is placed inside a template literal, inject a JavaScript expression using `${}`

6. Submit the payload through the search parameter

7. Load the response page

8. Observe that the JavaScript expression is evaluated and executes successfully

## Payload Used

${alert(1)}

## Result
Successfully executed arbitrary JavaScript by injecting an expression into a JavaScript template literal.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly escape user input before inserting it into JavaScript template literals
- Use context-aware output encoding
- Avoid embedding untrusted input into JavaScript code
- Implement Content Security Policy (CSP)
- Validate and sanitize all user-controlled input

## Learning
Escaping angle brackets, quotes, backslashes, and backticks alone is not sufficient to prevent XSS.
When user input is reflected inside JavaScript template literals, expressions enclosed in `${}` may still be evaluated, leading to arbitrary JavaScript execution.
