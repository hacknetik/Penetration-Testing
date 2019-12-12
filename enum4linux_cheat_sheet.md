# enum4linux

**Verbose mode, shows the underlying commands being executed by enum4linux**

`enum4linux -v target-ip`

#

**Do Everything, runs all options apart from dictionary based share name guessing**

`enum4linux -a target-ip`

#

**Lists usernames, if the server allows it - (RestrictAnonymous = 0)**

`enum4linux -U target-ip`

#

**If you've managed to obtain credentials, you can pull a full list of users regardless of the RestrictAnonymous option**

`enum4linux -u administrator -p password -U target-ip`

#

**Pulls usernames from the default RID range (500-550,1000-1050)**

`enum4linux -r target-ip`

#

**Pull usernames using a custom RID range**

`enum4linux -R 600-660 target-ip`

#

**Lists groups. if the server allows it, you can also specify username -u and password -p**

`enum4linux -G target-ip`

#

**List Windows shares, again you can also specify username -u and password -p**

`enum4linux -S target-ip`

#

**Perform a dictionary attack, if the server doesn't let you retrieve a share list**

`enum4linux -s shares.txt target-ip`

#

**Pulls OS information using smbclient, this can pull the service pack version on some versions of Windows**

`enum4linux -o target-ip`

#

**Pull information about printers known to the remove device.**

`enum4linux -i target-ip`

