All questions can be found [here](https://selectstarsql.com/hiatuses.html) <br>
\
1.Look up the documentation to fix the query so that it returns the number of days between the dates.
```
SELECT JULIANDAY('1993-08-10') - JULIANDAY('1989-07-07') AS day_difference ;
```
\
2.Write a query to produce the previous table.
Remember to use aliases to form the column names(ex_number, last_ex_date). Hint: Instead of shifting dates back, you could shift ex_number forward!
```
SELECT county, COUNT(ex_age) FROM executions
WHERE ex_age >= 50 
GROUP BY county ;
```

\
3.List the counties in which more than 2 inmates aged 50 or older have been executed.
```
-- this also returns the count of executions in each of those counties
SELECT county, COUNT(*) FROM executions
WHERE ex_age >= 50
GROUP BY county
HAVING COUNT(*) > 2 ;
```

\
4.List all the distinct counties in the dataset.
```
SELECT county FROM executions
GROUP BY county ;
```

\
5.Find the first and last name of the inmate with the longest last statement (by character count).
```
SELECT first_name, last_name
FROM executions
WHERE LENGTH(last_statement) =
    (SELECT MAX(LENGTH(last_statement)) FROM executions) ;
```

\
6.Write a query to find the percentage of executions from each county.
```
SELECT county, 100.0*COUNT(*) / (SELECT COUNT(*) FROM executions) AS Percent_Executions
FROM executions
GROUP BY county
ORDER BY Percent_Executions DESC ;
```
