# Lab Name
DOM XSS in jQuery anchor href attribute sink using location.search source

## Vulnerability
Cross-Site Scripting (XSS) – DOM-Based XSS

## Objective
Exploit a DOM-based XSS vulnerability by controlling an anchor's href attribute and execute JavaScript.

## Entry Point
URL query string (location.search)

## Exploitation Type
DOM-Based XSS

## Methodology
1. Open the lab and inspect the page source

2. Observe that user input is taken from:

   location.search

3. Notice that the value is inserted into an anchor tag's href attribute using jQuery

4. Since the input is not properly validated, it is possible to inject a JavaScript URI

5. Craft a payload using the javascript: protocol

6. Append the payload to the URL parameter

7. Load the page

8. Click the affected link on the page

9. Observe that the JavaScript executes in the browser

## Payload Used

javascript:alert(1)

## Result
Successfully executed arbitrary JavaScript through a DOM-based XSS vulnerability in a jQuery href attribute sink.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- User account compromise
- Manipulation of page content

## Mitigation
- Validate and sanitize user-controlled input
- Restrict dangerous URI schemes such as javascript:
- Use safe DOM APIs when assigning URLs
- Implement Content Security Policy (CSP)
- Perform allowlist-based URL validation

## Learning
Assigning user-controlled input directly to href attributes can lead to DOM-based XSS.
Applications should validate URL schemes and prevent the use of dangerous protocols such as javascript:.
