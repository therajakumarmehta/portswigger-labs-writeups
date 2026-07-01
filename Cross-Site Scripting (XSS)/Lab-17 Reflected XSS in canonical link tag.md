# Lab Name
Reflected XSS in canonical link tag

## Vulnerability
Cross-Site Scripting (XSS) – Reflected XSS

## Objective
Exploit a reflected XSS vulnerability by injecting a payload into the canonical link tag.

## Entry Point
URL parameter reflected in the canonical link tag

## Exploitation Type
Reflected XSS / Attribute Injection

## Methodology
1. Open the lab and inspect the page source

2. Observe that user input is reflected inside the canonical link tag

3. Notice that the input is inserted into the href attribute without proper sanitization

4. Craft a payload that injects an access key and an event handler

5. Append the payload to the URL

6. Load the page

7. Press the assigned access key to trigger the event

8. Observe that JavaScript executes successfully

## Payload Used

'accesskey='x'onclick='alert(1)

## Result
Successfully executed arbitrary JavaScript by injecting an event handler into the canonical link tag.

## Impact
- Execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise

## Mitigation
- Properly encode user input before inserting it into HTML attributes
- Validate and sanitize all user-controlled input
- Implement Content Security Policy (CSP)
- Use secure templating frameworks
- Avoid reflecting untrusted data into HTML attributes

## Learning
Even non-interactive HTML elements such as the canonical link tag can become XSS vectors if user input is reflected into their attributes without proper encoding and validation.
