---
title:  "[Basic join] Population Density Difference"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] Population Density Difference

> 문제

Query the difference between the maximum and minimum populations in CITY.

<br>

> 답

```sql
SELECT  MAX(POPULATION) - MIN(POPULATION)
FROM CITY
```

