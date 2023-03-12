## Join (take from two tables)
https://mariadb.com/kb/en/joining-tables-with-join-clauses/ <br>
https://mariadb.com/kb/en/join-syntax/
```
2 SETS, A and B (two tables)

# All from A, and matching from B (null if not matching) - Left outer join
SELECT * 
FROM tableA as A 
LEFT OUTER JOIN tableB as B 
ON A.myID = B.myID;

# All from B, and matching from A (null if not matching) - Right outer join (can do Left JOIN moving the syntax)
SELECT *
FROM tableA as A
RIGHT OUTER JOIN tableB as B
ON A.myID = B.myID;
    
```

## UNION (combine and remove duplicates)
The Union operator combines the results of two or more queries into a distinct single result set <br>
https://mariadb.com/kb/en/union/ <br>
https://www.sqlshack.com/sql-union-overview-usage-and-examples/
```
```

