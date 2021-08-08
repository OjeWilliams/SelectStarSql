These questions can be found [here](https://selectstarsql.com/questions.html)

1.Find the most networked senator. That is, the one with the most mutual cosponsorships.
A mutual cosponsorship refers to two senators who have each cosponsored a bill sponsored by the other. Even if a pair of senators have cooperated on many bills, the relationship still counts as one.


I attempted this with a CTE after reading the explaination [here](https://blog.sqlyog.com/window-functions-common-table-expressions-mysql-8-mariadb/)
````
WITH myCTE AS
(
SELECT DISTINCT(A.sponsor_name) AS Sen1, B.sponsor_name AS Sen2 
FROM cosponsors AS A 
JOIN cosponsors AS B 
ON A.sponsor_name = B.cosponsor_name
AND A.cosponsor_name = B.sponsor_name)

SELECT sen1, COUNT(*) AS ccount FROM myCTE
GROUP BY sen1
ORDER BY ccount DESC
LIMIT 1 ;
````

2.Now find the most networked senator from each state.
If multiple senators tie for top, show both. Return columns corresponding to state, senator and mutual cosponsorship count.
# took much longer thab expected and I need to review
```
WITH myCTE AS
( SELECT state, sen1, COUNT(*) as group_count 
 FROM(
SELECT DISTINCT(A.sponsor_name) AS Sen1,
B.sponsor_name AS Sen2, 
A.sponsor_state AS state
FROM cosponsors AS A 
JOIN cosponsors AS B 
ON A.sponsor_name = B.cosponsor_name
AND A.cosponsor_name = B.sponsor_name
      )
GROUP BY sen1, state),

-- Addressing max state counts 
myCTE2 AS(
SELECT state, MAX(group_count) AS Max_count
  FROM myCTE
  GROUP BY state
)

SELECT myCTE.state, sen1, Max_count FROM myCTE
JOIN myCTE2 
ON myCTE.state = myCTE2.state
AND myCTE.group_count = myCTE2.Max_count
GROUP BY sen1
ORDER BY group_count DESC
;

```
