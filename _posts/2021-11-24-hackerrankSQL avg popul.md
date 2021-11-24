---
title:  "[Basic join] Average Population of Each Continent"
excerpt: "Difficulty : easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-24
---

# [Basic join] Average Population of Each Continent

> 문제

Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.
<br>

> 답

```sql
SELECT T.CONTINENT, FLOOR(AVG(c.POPULATION))
FROM CITY as c INNER JOIN COUNTRY as T ON c.COUNTRYCODE = T.CODE
GROUP BY CONTINENT
```

