# Lab Name
SSRF with blacklist-based input filter

## Vulnerability
Server-Side Request Forgery (SSRF) – Blacklist Filter Bypass

## Objective
Bypass the application's blacklist-based URL filter to access the internal admin panel and delete the user Carlos.

## Entry Point
Check Stock functionality

## Exploitation Type
Server-Side Request Forgery (SSRF)

## Methodology
1. Open the lab in Burp's browser.

2. Navigate to any product page and click the **Check stock** button.

3. Intercept the stock check request using **Burp Suite Proxy**.

4. Send the request to **Burp Repeater**.

5. Locate the **stockApi** parameter and replace its value with:

```text
http://127.0.0.1/
```

6. Send the request and observe that access to **127.0.0.1** is blocked by the application's blacklist.

7. Bypass the IP address filter by replacing the URL with:

```text
http://127.1/ (2130706433/017700000001)
```

8. Send the request and observe that the request is now accepted because **127.1** resolves to **127.0.0.1**.

9. Attempt to access the admin interface:

```text
http://127.1/admin
```

10. Send the request and observe that access is blocked again because the application filters the **admin** path.

11. Bypass the blacklist by double URL-encoding the letter **a** in **admin**:

```text
http://127.1/%2561dmin
```

12. Send the request.

13. Observe that the internal **Admin** interface is returned.

14. Read the HTML response and identify the endpoint used to delete Carlos.

```text
http://127.1/%2561dmin/delete?username=carlos
```

15. Replace the **stockApi** parameter with the delete endpoint.

```text
http://127.1/%2561dmin/delete?username=carlos
```

16. Send the request.

17. Observe that Carlos is deleted successfully.

18. Return to the lab page and verify that the lab has been solved.

## Payload Used

### Bypass Localhost Filter

```text
http://127.1/
```

### Access Admin Panel

```text
http://127.1/%2561dmin
```

### Delete Carlos

```text
http://127.1/%2561dmin/delete?username=carlos
```

## Result
Successfully bypassed the application's blacklist-based URL filter, accessed the internal admin interface, deleted the user Carlos, and solved the lab.

## Impact
- Access to internal services
- Bypass of blacklist-based security controls
- Unauthorized administrative actions
- Exposure of internal applications
- Potential compromise of internal infrastructure

## Mitigation
- Use strict allowlists instead of blacklists for URL validation.
- Block requests to loopback and private IP ranges after canonicalization.
- Normalize and decode URLs before applying security checks.
- Restrict outbound requests to trusted destinations only.
- Isolate internal administrative services from user-controlled requests.

## Learning
This vulnerability demonstrates that blacklist-based URL filtering is unreliable. The application blocked requests to **127.0.0.1** and **/admin**, but these protections were bypassed by using the alternative loopback address **127.1** and double URL encoding (`%2561`) to evade path filtering. Proper URL normalization and allowlist validation are essential to prevent SSRF bypass techniques.
