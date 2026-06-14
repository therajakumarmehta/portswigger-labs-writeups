# Lab Name
Stored XSS into HTML context with nothing encoded

## Vulnerability
Cross-Site Scripting (XSS) – Stored XSS

## Objective
Store a malicious script in the application that executes when viewed by other users.

## Entry Point
Comment functionality (or any input field that stores data)

## Exploitation Type
Stored XSS / Persistent XSS

## Methodology
1. Open the lab and locate a feature that stores user input (e.g., comment section)

2. Submit a normal comment and observe how it is displayed

3. Notice that the input is stored and rendered without encoding

4. Inject a malicious payload in the input field:

   <script>alert(1)</script>

5. Submit the comment

6. When the page reloads or when another user views the comment, the script executes

## Payload Used

<script>alert(1)</script>

## Result
Successfully stored a malicious script that executes whenever the page is viewed.

## Impact
- Persistent execution of malicious JavaScript
- Session hijacking
- Cookie theft
- Defacement of web pages
- Targeting multiple users (including admin)

## Mitigation
- Encode output before rendering user input
- Sanitize input on the server side
- Use Content Security Policy (CSP)
- Validate and filter dangerous input
- Use secure frameworks with built-in XSS protection

## Learning
Stored XSS is more dangerous than reflected XSS because it affects all users who view the affected page.
Proper input validation and output encoding are critical to prevent such attacks.
