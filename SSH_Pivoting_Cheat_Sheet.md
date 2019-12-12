# SSH Pivoting

### SSH Port Forwarding

#

Port 8080 locally is forwarded to port 443 on 10.0.0.1 through host 192.168.1.160

`ssh -L 8080:10.0.0.1:443 user@192.168.1.160`

#

### SSH Port Forwarding with Proxychains

Dynamically allows all port forwards to the subnets availble on the target.

`ssh -D 127.0.0.1:9050 root@192.168.1.160`

_*Dynamic Proxychain SSH port forwarding does not work with nmap and metasploits meterpreter shells won't spawn.*_

_*If you attempt to spawn a shell via Meterpreter, you’ll get an error similar to the following:*_

`meterpreter > execute -f cmd.exe -i -H
|S-chain|-<>-127.0.0.1:9050-<><>-127.0.0.1:41713-<--timeout`

#

### Meterpreter Pivoting

Forwards 3389 (RDP) to 3389 on the compromised machine running the Meterpreter shell

`portfwd add –l 3389 –p 3389 –r target-host`

#

Forwards 3389 (RDP) to 3389 on the compromised machine running the Meterpreter shell

`portfwd delete –l 3389 –p 3389 –r target-host`

#

Delete all port forwards

`portfwd flush`

#

List active port forwards

`portfwd list`

#

Autoroute script to add the route for specified subnet 192.168.15.0

run autoroute -s 192.168.15.0/24

#

List all active routes

`run autoroute -p`

#

View available networks the compromised host can access

`route`

#

Add route for 192.168.14.0/24 via Session 3.

`route add 192.168.14.0 255.255.255.0 3`

#

Delete route for 192.168.14.0/24 via Session 3.

`route delete 192.168.14.0 255.255.255.0 3`

#

Delete all routes

`route flush`






