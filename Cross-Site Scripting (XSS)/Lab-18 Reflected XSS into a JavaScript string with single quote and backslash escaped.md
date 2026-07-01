# Lab Name
Reflected XSS into a JavaScript string with single quote and backslash escaped

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Exploit a reflected XSS vulnerability by breaking out of a JavaScript string despite single quotes and backslashes being escaped.

## Entry Point
Search functionality

## Exploitation Type
Reflected XSS / JavaScript Context Injection

## Methodology
1. Open the lab and locate the search functionality

2. Submit a normal search request

3. Observe that the search term is reflected inside a JavaScript string

4. Notice that single quotes and backslashes are escaped by the application

5. Craft a payload that safely breaks out of the JavaScript string and injects executable JavaScript

6. Submit the payload through the search parameter

7. Load the response page

8. Observe that the injected JavaScript executes successfully

## Payload Used

</script><script>alert(1)</script>

## Result
Successfully executed arbitrary JavaScript by breaking out of the JavaScript context.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly escape user input for JavaScript contexts
- Use context-aware output encoding
- Avoid inserting user input directly into JavaScript code
- Implement Content Security Policy (CSP)
- Validate and sanitize all user-controlled input

## Learning
Escaping single quotes and backslashes alone is not enough to prevent XSS.
If user input is reflected inside a JavaScript context, attackers may still escape the context using alternative techniques such as closing the script tag and injecting a new script block.
