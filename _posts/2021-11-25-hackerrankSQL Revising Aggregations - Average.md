---
title:  "[Basic join] Revising Aggregations - Averages"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] Revising Aggregations - Averages

> 문제

Query the average population of all cities in CITY where District is California.

<br>

> 답

```sql
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT = 'California'
```

