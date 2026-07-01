# Lab Name
Reflected XSS into a JavaScript string with angle brackets and double quotes HTML-encoded and single quotes escaped

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Exploit a reflected XSS vulnerability by breaking out of a JavaScript string despite angle brackets and double quotes being HTML-encoded and single quotes being escaped.

## Entry Point
Search functionality

## Exploitation Type
Reflected XSS / JavaScript Context Injection

## Methodology
1. Open the lab and locate the search functionality

2. Submit a normal search request

3. Observe that the search term is reflected inside a JavaScript string

4. Notice that:
   - Angle brackets (< and >) are HTML-encoded
   - Double quotes (") are HTML-encoded
   - Single quotes (') are escaped

5. Craft a payload that breaks out of the JavaScript string without relying on angle brackets or double quotes

6. Inject the payload into the search parameter

7. Submit the request

8. Load the response page

9. Observe that the injected JavaScript executes successfully

## Payload Used

\'-alert(1)// 

## Result
Successfully executed arbitrary JavaScript by escaping the JavaScript string and injecting executable code.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly escape user input for JavaScript contexts
- Use context-aware output encoding
- Avoid embedding user input directly into JavaScript code
- Implement Content Security Policy (CSP)
- Validate and sanitize all user-controlled input

## Learning
Encoding angle brackets and double quotes alone is not sufficient to prevent XSS.
When user input is reflected inside a JavaScript string, improper escaping can still allow attackers to break out of the string and execute arbitrary JavaScript.
