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

```
