# Lab Name
Username enumeration via response time

## Vulnerability
Authentication flaw – Username enumeration through timing discrepancy

## Objective
Identify valid usernames by measuring differences in server response time during login attempts.

## Entry Point
Login form (username parameter)

## Exploitation Type
Username enumeration via response time analysis

## Methodology
1. Intercepted the login request using a proxy tool.
2. Sent login attempts with different usernames while keeping the password constant.
3. Measured and compared response times.
4. Repeated each request multiple times to confirm consistency.
5. Avoided rapid requests to prevent triggering rate limits and IP blocking.

## Payload Used
Username: candidate usernames tested sequentially  
Password: constant dummy value (e.g., test123)

## Observation
- Non-existing usernames returned responses quickly.
- A specific username consistently produced slower responses.
- The delay was reproducible across multiple attempts.
- Excessive rapid requests triggered temporary IP blocking due to rate limiting.

## Result
Successfully identified a valid username based on consistent response time differences.

## Root Cause
The application performs password hashing and comparison only when the username exists.
If the username does not exist, the process terminates early, resulting in faster responses.

## Impact
An attacker can enumerate valid usernames without visible message differences.
This significantly increases the effectiveness of brute-force and credential stuffing attacks.

## Mitigation
- Implement constant-time authentication checks.
- Ensure identical processing paths for valid and invalid usernames.
- Apply proper rate limiting and monitoring.
- Return uniform response times and messages.

## Learning
- Timing attacks do not rely on visible error messages.
- Even small processing differences can leak sensitive information.
- Rate limiting and IP blocking are defensive mechanisms but do not eliminate timing flaws.
- Always verify timing discrepancies through repeated testing.
