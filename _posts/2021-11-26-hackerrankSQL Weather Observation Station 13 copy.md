---
title:  "[Basic join] Weather Observation Station 13"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-26
last_modified_at: 2021-11-26
---

# [Basic join] Weather Observation Station 13

> 문제

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38,7880 and less than 137,2345. Truncate your answer to 4 decimal places.

<br>


> 답

```sql
SELECT TRUNCATE(SUM(LAT_N),4)
FROM STATION
WHERE LAT_N BETWEEN '38.7880' AND '137.2345'
```

