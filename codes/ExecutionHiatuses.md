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
SELECT ex_number + 1 AS ex_number, ex_date AS last_ex_date
FROM executions
WHERE ex_number < 553 ;
```

\
3.Nest the query which generates the previous table into the template.
Notice that we are using a table alias here, naming the result of the nested query "previous".
```
SELECT
  last_ex_date AS start,
  ex_date AS end,
  JULIANDAY(ex_date) - JULIANDAY(last_ex_date)
    AS day_difference
FROM executions
JOIN (SELECT ex_number + 1 AS ex_number, ex_date AS last_ex_date
FROM executions
WHERE ex_number < 553 ) AS previous
  ON executions.ex_number = previous.ex_number
ORDER BY day_difference DESC
LIMIT 10 ;
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
