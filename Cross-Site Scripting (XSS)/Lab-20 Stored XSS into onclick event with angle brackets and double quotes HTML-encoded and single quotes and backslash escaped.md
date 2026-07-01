# Lab Name
Stored XSS into onclick event with angle brackets and double quotes HTML-encoded and single quotes and backslash escaped

## Vulnerability
Cross-Site Scripting (XSS) – Stored XSS

## Objective
Exploit a stored XSS vulnerability by injecting JavaScript into an onclick event despite multiple character encodings.

## Entry Point
Comment functionality

## Exploitation Type
Stored XSS / JavaScript Context Injection

## Methodology
1. Open the lab and navigate to the comment section

2. Submit a normal comment and observe how it is rendered

3. Notice that user input is stored inside an onclick event

4. Observe that:
   - Angle brackets (< and >) are HTML-encoded
   - Double quotes (") are HTML-encoded
   - Single quotes (') and backslashes (\) are escaped

5. Craft a payload that breaks out of the JavaScript string and injects executable JavaScript

6. Submit the payload in the comment field

7. Publish the comment

8. Click the affected element containing the onclick event

9. Observe that the injected JavaScript executes successfully

## Payload Used

&#39;-alert(1)-&#39;

## Result
Successfully executed arbitrary JavaScript through a stored XSS vulnerability in an onclick event.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly escape user input for JavaScript contexts
- Use context-aware output encoding
- Avoid inserting untrusted input into event handlers
- Implement Content Security Policy (CSP)
- Validate and sanitize all user-controlled input

## Learning
Escaping angle brackets, quotes, and backslashes alone is not sufficient to prevent XSS.
When user input is embedded inside JavaScript event handlers, improper context-aware encoding can still allow attackers to execute arbitrary JavaScript.
