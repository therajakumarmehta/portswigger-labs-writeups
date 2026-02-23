# Lab Name
Username enumeration via subtly different responses

## Vulnerability
Authentication flaw – Username enumeration

## Objective
Identify valid usernames by observing subtle differences in login responses.

## Entry Point
Login form (username parameter)

## Exploitation Type
Username enumeration via subtle response variation

## Methodology
1. Intercepted login requests using proxy.
2. Sent login attempts with various usernames while keeping password constant.
3. Compared server responses for existing and non-existing usernames.
4. Observed subtle differences in response behavior.

## Payload Used
Username: valid_username (identified through response variation)
Password: random_password

## Observation
- Login attempts with non-existing usernames returned identical error messages and response lengths.
- Login attempts with valid usernames returned a slightly different response:
  - Change in error message wording
  - Different response length
  - Variation in HTTP status or page structure

## Result
Successfully identified a valid username based on subtle response differences.

## Impact
An attacker can enumerate valid usernames before performing password attacks such as brute force or credential stuffing.

## Learning
- Applications should return identical responses for both invalid usernames and incorrect passwords.
- Even small differences (extra space, punctuation, response length, status code) can leak account existence.
- Response comparison tools (e.g., proxy comparison features) help detect subtle variations.
- Proper authentication design must prevent information disclosure through inconsistent behavior.
- Security testing should always include response diff analysis when testing login functionality.
