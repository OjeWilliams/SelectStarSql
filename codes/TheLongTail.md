All questions can be found [here](https://selectstarsql.com/longtail.html) \

1.Modify this query so there are up to two rows per county — one counting executions with a last statement and another without.
```
SELECT
  county,
  COUNT(*)
FROM executions
GROUP BY county

###My attempt###
SELECT
  county,
  last_statement IS NOT NULL AS no_statement,
  COUNT(last_statement)
FROM executions
GROUP BY county, no_statement ;

```

2.Count the number of inmates aged 50 or older that were executed in each county.
```
SELECT county, COUNT(ex_age) FROM executions
WHERE ex_age >= 50 
GROUP BY county ;
```
