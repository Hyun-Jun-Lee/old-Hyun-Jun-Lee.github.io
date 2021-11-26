---
title:  "[Basic join] Weather Observation Station 14"
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

Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345. Truncate your answer to 4 decimal places.
<br>


> 답

```sql
SELECT TRUNCATE(MAX(LAT_N),4)
FROM STATION
WHERE LAT_N < '137.2345'
```

