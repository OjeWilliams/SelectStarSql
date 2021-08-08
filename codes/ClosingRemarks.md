These questions can be found [here](https://selectstarsql.com/questions.html)

1.Find the most networked senator. That is, the one with the most mutual cosponsorships.
A mutual cosponsorship refers to two senators who have each cosponsored a bill sponsored by the other. Even if a pair of senators have cooperated on many bills, the relationship still counts as one.
````
-- I attempted this with a CTE after reading the explaination [here](https://blog.sqlyog.com/window-functions-common-table-expressions-mysql-8-mariadb/)
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
