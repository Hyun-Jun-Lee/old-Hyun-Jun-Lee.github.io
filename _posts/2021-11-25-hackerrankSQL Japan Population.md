---
title:  "[Basic join] Japan Population"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] Japan Population

> 문제

Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

<br>

> 답

```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE = 'JPN'
```

