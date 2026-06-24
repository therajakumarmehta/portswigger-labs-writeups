# Lab Name
Stored DOM XSS

## Vulnerability
Cross-Site Scripting (XSS) – Stored DOM-Based XSS

## Objective
Exploit a stored DOM-based XSS vulnerability and execute JavaScript in the victim's browser.

## Entry Point
Stored user input in comments

## Exploitation Type
Stored DOM-Based XSS

## Methodology
1. Open the lab and identify a feature that stores user input

2. Submit a normal input and observe how it is displayed

3. Inspect the page source and client-side JavaScript

4. Notice that stored data is retrieved and processed by JavaScript in the browser

5. Identify a vulnerable DOM sink (such as innerHTML)

6. Inject a malicious payload into the stored input field

7. Submit and save the payload

8. When the page reloads or another user visits the page, the stored data is processed by client-side JavaScript

9. Observe that the payload executes automatically

## Payload Used

<img src=x onerror=alert(1)>

## Result
Successfully stored a malicious payload that executes JavaScript whenever the affected page is viewed.

## Impact
- Persistent execution of arbitrary JavaScript
- Session hijacking
- Cookie theft
- Phishing attacks
- Account compromise
- Targeting multiple users including administrators

## Mitigation
- Sanitize and validate all user-controlled input
- Avoid inserting untrusted data into dangerous DOM sinks
- Use textContent instead of innerHTML where possible
- Implement Content Security Policy (CSP)
- Perform both server-side and client-side validation

## Learning
Stored DOM XSS occurs when malicious input is stored by the application and later processed insecurely by client-side JavaScript.
Because the payload is persistent, it can affect every user who views the vulnerable page, making it more dangerous than reflected DOM XSS.
