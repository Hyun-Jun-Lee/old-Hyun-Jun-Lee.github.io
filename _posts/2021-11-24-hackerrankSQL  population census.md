---
title:  "[Basic join] Population Census"
excerpt: "Difficulty : easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-24
---

# [advance Select] Type of Triangle

> 문제

Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

<br>

> 답

```sql
SELECT SUM(c.POPULATION)
FROM CITY as c INNER JOIN COUNTRY as T ON c.COUNTRYCODE = T.CODE
WHERE T.CONTINENT = 'Asia'
```

