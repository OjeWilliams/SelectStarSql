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
4.Fill in the JOIN ON clause to complete a more elegant version of the previous query.
```
SELECT
  previous.ex_date AS start,
  executions.ex_date AS end,
  JULIANDAY(executions.ex_date) - JULIANDAY(previous.ex_date)
    AS day_difference
FROM executions
JOIN executions AS previous
  ON executions.ex_number = previous.ex_number + 1
ORDER BY day_difference DESC
LIMIT 10 ;
```
