# Lab Name
Reflected XSS into HTML context with nothing encoded

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Execute JavaScript in the victim's browser by injecting a malicious payload.

## Entry Point
Search functionality (URL parameter)

## Exploitation Type
Reflected XSS / Input Injection

## Methodology
1. Open the lab and locate the search functionality

2. Enter a normal search query and observe how it is reflected in the response

3. Notice that the input is reflected directly into HTML without encoding

4. Inject a simple XSS payload in the search parameter:

   <script>alert(1)</script>

5. Submit the request

6. Observe that the script executes in the browser

## Payload Used

<script>alert(1)</script>

## Result
Successfully executed JavaScript in the browser via reflected XSS.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Full control over user interaction

## Mitigation
- Encode all user input before rendering in HTML
- Use proper output encoding (HTML encoding)
- Implement Content Security Policy (CSP)
- Validate and sanitize user input
- Use secure frameworks that prevent XSS by default

## Learning
User input must never be directly reflected into HTML without encoding.
Proper output encoding is essential to prevent XSS vulnerabilities.
