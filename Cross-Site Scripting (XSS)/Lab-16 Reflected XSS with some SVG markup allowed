# Lab Name
Reflected XSS with some SVG markup allowed

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Exploit a reflected XSS vulnerability by using allowed SVG markup to execute JavaScript.

## Entry Point
Search functionality

## Exploitation Type
Reflected XSS / SVG-Based XSS

## Methodology
1. Open the lab and locate the search functionality

2. Test standard XSS payloads and observe that most HTML tags are blocked

3. Notice that some SVG elements and attributes are still allowed

4. Craft an SVG payload using an event handler

5. Inject the payload into the search parameter

6. Submit the request

7. Observe that the SVG event is triggered and JavaScript executes successfully

## Payload Used

<svg><animatetransform onbegin=alert(1) attributeName=transform>

## Result
Successfully executed arbitrary JavaScript using allowed SVG markup despite the application's filtering.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly sanitize SVG content
- Remove dangerous SVG elements and event handlers
- Use context-aware output encoding
- Implement Content Security Policy (CSP)
- Validate and sanitize all user-controlled input

## Learning
Blocking only common HTML tags is not enough to prevent XSS.
SVG elements can also execute JavaScript if dangerous attributes or event handlers are allowed, making proper input validation and output encoding essential.
