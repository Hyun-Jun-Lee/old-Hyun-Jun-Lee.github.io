---
title:  "[Basic join] Average Population"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] Average Population

> 문제

Query the average population for all cities in CITY, rounded down to the nearest integer.

<br>

> 답

```sql
SELECT FLOOR(AVG(POPULATION))
FROM CITY
```

