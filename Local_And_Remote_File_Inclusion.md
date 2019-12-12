# Local and Remote File Inclusion (LFI/RFI)


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
