These questions can be found [here](https://selectstarsql.com/beazley.html)

1.Find the first and last names and ages (ex_age) of inmates 25 or younger at time of execution.
```
SELECT first_name, last_name, ex_age
FROM executions
WHERE ex_age <= 25 ;
```
\
2.Modify the query to find the result for Raymond Landry. \
We needed to ensure that we checked for something attached to his name like Snr or Jnr.
```
SELECT first_name, last_name, ex_number
FROM executions
WHERE first_name LIKE 'Raymond'
  AND last_name LIKE 'Landry%' ;
```
\
3.Insert a pair of parenthesis so that this statement returns 0.
`SELECT 0 AND (0 OR 1) ; `

\
4.Find Napoleon Beazley's last statement.
```
SELECT last_statement
FROM executions
WHERE first_name LIKE 'Napoleon' 
	AND last_name LIKE 'Beazley' ;
```
