# Lab Name
Basic SSRF against the local server

## Vulnerability
Server-Side Request Forgery (SSRF)

## Objective
Exploit the stock check functionality to make the server send requests to the internal localhost server and delete the user Carlos.

## Entry Point
Check Stock functionality

## Exploitation Type
Server-Side Request Forgery (SSRF)

## Methodology
1. Open the lab and log in using the provided user credentials (if required).

2. Navigate to any product page.

3. Click the **Check stock** button.

4. Intercept the stock check request using **Burp Suite Proxy**.

5. Observe that the request contains a parameter similar to:

```http
stockApi=http://stock.weliketoshop.net:8080/product/stock/check?productId=1&storeId=1
```

6. Send the request to **Burp Repeater**.

7. Replace the **stockApi** URL with the localhost address.

```text
http://localhost/
```

8. Send the request.

9. Observe that the application successfully accesses the internal web server, confirming that the backend server can communicate with localhost.

10. Enumerate the available internal endpoints by modifying the URL.

```text
http://localhost/admin
```

11. Send the request and observe that the internal **Admin** panel is accessible.

12. Review the response and identify the endpoint used to delete Carlos.

Example:

```text
http://localhost/admin/delete?username=carlos
```

13. Replace the **stockApi** value with the discovered endpoint.

```text
http://localhost/admin/delete?username=carlos
```

14. Send the request.

15. Observe that the response indicates Carlos has been deleted successfully.

16. Return to the lab page and verify that the lab is solved.

## Payload Used

### Access Localhost

```text
http://localhost/
```

### Access Admin Panel

```text
http://localhost/admin
```

### Delete Carlos

```text
http://localhost/admin/delete?username=carlos
```

## Result
Successfully exploited the Server-Side Request Forgery vulnerability to access the internal localhost server, reached the hidden admin interface, deleted the user Carlos, and solved the lab.

## Impact
- Access to internal services
- Bypass of network access controls
- Exposure of internal applications
- Unauthorized administrative actions
- Potential Remote Code Execution depending on accessible internal services

## Mitigation
- Validate and strictly whitelist outbound URLs.
- Block requests to localhost and private IP ranges.
- Disable unnecessary outbound network access from the application server.
- Implement network segmentation to isolate internal services.
- Validate user-supplied URLs before making server-side requests.

## Learning
This vulnerability occurs because the application allows user-controlled URLs to be requested by the server without proper validation. By changing the **stockApi** parameter to point to **localhost**, an attacker can access internal services that are not publicly exposed. In this lab, the SSRF vulnerability is used to reach the hidden admin panel and perform an unauthorized administrative action by deleting the user Carlos.
