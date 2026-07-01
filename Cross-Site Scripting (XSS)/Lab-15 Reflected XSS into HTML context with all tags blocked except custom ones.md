# Lab Name
Reflected XSS into HTML context with all tags blocked except custom ones

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS with Custom Tag Bypass

## Objective
Exploit a reflected XSS vulnerability by using custom HTML elements when standard HTML tags are blocked.

## Entry Point
Search functionality

## Exploitation Type
Reflected XSS / Filter Bypass 

## Methodology
1. Open the lab and locate the search functionality.

2. Test common XSS payloads and observe that all standard HTML tags are blocked.

3. Notice that custom HTML elements are not filtered by the application's validation.

4. Create a custom HTML element and attach an event handler that can execute JavaScript.

5. Inject the payload into the search parameter.

6. Submit the request.

7. Trigger the event (e.g., by focusing the element or using an autofocus attribute).

8. Observe that JavaScript executes successfully.

## Payload Used

<xss id=x tabindex=1 autofocus onfocus=alert(1) >

## Result
Successfully bypassed the HTML tag filter using a custom HTML element and executed arbitrary JavaScript.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Do not rely on blacklist-based filtering of HTML tags.
- Sanitize user input using a robust allowlist-based HTML sanitizer.
- Encode user input according to the output context.
- Implement Content Security Policy (CSP).
- Validate and sanitize all user-controlled input before rendering.

## Learning
Blocking only predefined HTML tags is not sufficient to prevent XSS.
Modern browsers support custom HTML elements, which attackers can abuse to inject event handlers and execute JavaScript if proper output encoding and sanitization are not implemented.
