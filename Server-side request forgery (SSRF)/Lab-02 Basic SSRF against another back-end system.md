# Lab Name
Basic SSRF against another back-end system

## Vulnerability
Server-Side Request Forgery (SSRF)

## Objective
Exploit the stock check functionality to access an internal back-end system, identify the admin interface, delete the user Carlos, and solve the lab.

## Entry Point
Check Stock functionality

## Exploitation Type
Server-Side Request Forgery (SSRF)

## Methodology
1. Open the lab in Burp's browser.

2. Navigate to any product page and click the **Check stock** button.

3. Intercept the stock check request using **Burp Suite Proxy**.

4. Send the request to **Burp Repeater**.

5. Observe the **stockApi** parameter, which contains the URL used by the server to perform the stock check.

6. Since the admin interface is hosted on another internal back-end system, begin enumerating the internal IP range.

7. Replace the **stockApi** value with the following format and test each IP address:

```text
http://192.168.0.X:8080/admin
```

8. Use **Burp Intruder** to automate the enumeration.

- Target:

```text
http://192.168.0.§1§:8080/admin
```

- Payload Type:

```text
Numbers
```

- Payload Range:

```text
1 - 255
```

9. Start the Intruder attack.

10. Review the responses and identify the IP address that returns the **Admin** interface instead of an error or redirect.

Example:

```text
http://192.168.0.42:8080/admin
```

11. Open the successful response and identify the endpoint used to delete Carlos.

Example:

```text
http://192.168.0.42:8080/admin/delete?username=carlos
```

12. Replace the **stockApi** parameter with the discovered delete endpoint.

```text
http://192.168.0.42:8080/admin/delete?username=carlos
```

13. Send the request.

14. Observe that Carlos is deleted successfully.

15. Return to the lab page and verify that the lab has been solved.

## Payload Used

### Internal Network Scan

```text
http://192.168.0.X:8080/admin
```

### Delete Carlos

```text
http://192.168.0.42:8080/admin/delete?username=carlos
```

## Result
Successfully exploited the SSRF vulnerability to access an internal back-end system, discovered the hidden admin interface, deleted the user Carlos, and solved the lab.

## Impact
- Access to internal network services
- Internal network enumeration
- Unauthorized administrative actions
- Exposure of internal applications
- Potential compromise of internal infrastructure

## Mitigation
- Strictly validate and whitelist outbound URLs.
- Block requests to private and loopback IP ranges.
- Restrict server-side requests to trusted destinations only.
- Isolate internal administrative services from application servers.
- Monitor and log outbound requests for SSRF attempts.

## Learning
This vulnerability demonstrates that SSRF can be used not only to access **localhost**, but also to reach other systems within an organization's internal network. By enumerating private IP addresses, an attacker can discover hidden administrative interfaces and perform unauthorized actions that are inaccessible from the public internet.
