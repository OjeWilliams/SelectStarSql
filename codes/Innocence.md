Questions can be found [here](https://selectstarsql.com/innocence.html)

1.Find the total number of executions in the dataset.
```
SELECT COUNT(*) FROM executions ;
```
\
2.This query counts the number of Harris and Bexar county executions. Replace SUMs with COUNTs and edit the CASE WHEN blocks so the query still works.
```
-- original code
SELECT
    SUM(CASE WHEN county='Harris' THEN 1
        ELSE 0 END),
    SUM(CASE WHEN county='Bexar' THEN 1
        ELSE 0 END)
FROM executions

-- edited code
SELECT
    COUNT(CASE WHEN county='Harris' THEN 1
        ELSE NULL END),
    COUNT(CASE WHEN county='Bexar' THEN 1
        ELSE NULL END)
FROM executions ;
```

\
3.Find how many inmates were over the age of 50 at execution time.

```
SELECT
COUNT(CASE WHEN ex_age > 50 THEN 1
	 ELSE NULL
END)
FROM executions ;
```

\
4. Find the number of inmates who have declined to give a last statement.
For bonus points, try to do it in 3 ways:
1) With a WHERE block,
2) With a COUNT and CASE WHEN block,
3) With two COUNT functions.

-- WHERE
```
SELECT COUNT(*) FROM executions
WHERE last_statement is NULL ;
```
-- Count and Case When Block

```
SELECT
COUNT(CASE WHEN last_statement is NULL THEN 1
	  ELSE NULL
END)
FROM executions;
```
