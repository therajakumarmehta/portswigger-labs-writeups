# Lab Name
Username enumeration via different response behavior

## Vulnerability
Authentication logic - username enumeration

## Objective
Determine which usernames exist based on differences in application responses.

## Entry Point
Login form (username input)

## Exploitation Type
Username enumeration through conditional response observation.

## Payload Used
Valid existing username and non-existing username test inputs to observe behavior changes.

## Result
Identified which usernames exist in the system based on distinct responses to login attempts.

## Learning
- Username enumeration vulnerabilities occur when the application returns distinguishable responses for existing vs non-existing usernames.
- Differences in error messages, status codes, or page content reveal information about valid accounts.
- This flaw allows attackers to identify valid usernames before attempting further attacks.
- Input validation and generic error messages should be implemented to prevent disclosure of account existence.
- Consistent response timing and messages help prevent account enumeration attacks.
