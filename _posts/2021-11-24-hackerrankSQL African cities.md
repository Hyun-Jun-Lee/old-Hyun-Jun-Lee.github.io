---
title:  "[Basic join] African Cities"
excerpt: "Difficulty : easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-24
---

# [advance Select] African Cities

> 문제

Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

<br>

> 답

```sql
SELECT c.NAME
FROM CITY as c INNER JOIN COUNTRY as T ON c.COUNTRYCODE = T.CODE
WHERE T.CONTINENT = 'Africa'
```

