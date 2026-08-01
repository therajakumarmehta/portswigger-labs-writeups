# Lab Name
Web shell upload via Content-Type restriction bypass

## Vulnerability
Unrestricted File Upload – Content-Type Validation Bypass

## Objective
Bypass the application's Content-Type validation, upload a malicious PHP file, execute it on the server, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Remote Code Execution (RCE)

## Methodology
1. Open Burp's browser and log in using the provided user credentials.

2. Navigate to the **My Account** page and upload any valid image as your avatar.

3. Return to the account page and verify that the uploaded avatar is displayed successfully.

4. In **Burp Suite**, go to **Proxy > HTTP History** and locate the request used to fetch your avatar.

Example:

```http
GET /files/avatars/your-image.jpg HTTP/1.1
```

5. Send the **GET** request to **Burp Repeater**.

6. On your local machine, create a file named **exploit.php** with the following content:

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

7. Attempt to upload **exploit.php** as your avatar.

8. Observe that the server rejects the upload because only files with the MIME type **image/jpeg** or **image/png** are allowed.

9. In **Burp Suite**, locate the **POST /my-account/avatar** request in **HTTP History** and send it to **Burp Repeater**.

10. In the Repeater tab containing the upload request, locate the file section of the multipart request and change the **Content-Type** header from:

```http
Content-Type: application/x-php
```

to:

```http
Content-Type: image/jpeg
```

11. Send the modified request.

12. Observe that the server accepts the upload and stores the PHP file successfully.

13. Switch to the Repeater tab containing the avatar retrieval request.

14. Replace the image filename with **exploit.php**.

```http
GET /files/avatars/exploit.php HTTP/1.1
```

15. Send the request.

16. Observe that the server executes the uploaded PHP file and returns the contents of **/home/carlos/secret** in the response.

17. Copy the secret and submit it to complete the lab.

## Payload Used

### PHP File

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### Modified Upload Header

```http
Content-Type: image/jpeg
```

### Request

```http
GET /files/avatars/exploit.php HTTP/1.1
```

## Result
Successfully bypassed the MIME type restriction by modifying the **Content-Type** header, uploaded a malicious PHP file, executed it on the server, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- Arbitrary file upload
- Sensitive file disclosure
- Server compromise
- Potential full system compromise

## Mitigation
- Validate uploaded files using server-side file signature (magic bytes) verification instead of trusting the **Content-Type** header.
- Restrict uploads to a strict allowlist of safe file types.
- Store uploaded files outside the web root.
- Disable script execution in upload directories.
- Rename uploaded files and remove executable extensions before storage.
- Perform comprehensive server-side validation on every uploaded file.

## Learning
Relying solely on the **Content-Type** header for file validation is insecure because it is entirely controlled by the client and can be modified using tools such as Burp Suite. Applications should verify the actual file type using server-side validation techniques and ensure that uploaded files cannot be executed as server-side scripts.
