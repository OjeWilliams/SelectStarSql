These questions can be found [here](https://selectstarsql.com/beazley.html)

1.Find the first and last names and ages (ex_age) of inmates 25 or younger at time of execution.
```
SELECT first_name, last_name, ex_age
FROM executions
WHERE ex_age <= 25 ;
```
