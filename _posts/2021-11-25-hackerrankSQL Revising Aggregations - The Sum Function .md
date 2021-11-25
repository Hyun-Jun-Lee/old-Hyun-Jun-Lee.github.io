---
title:  "[Basic join] Revising Aggregations - The Sum Function"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-25
---

# [Basic join] Revising Aggregations - The Sum Function

> 문제

Query the total population of all cities in CITY where District is California.


<br>

> 답

```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT = 'California'
```

