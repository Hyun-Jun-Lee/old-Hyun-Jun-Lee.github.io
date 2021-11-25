---
title:  "[Basic join] Aggregation"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-25
---

# [Basic join] Aggregation

> 문제

Query a count of the number of cities in CITY having a Population larger than 100,000 .


<br>

> 답

```sql
SELECT COUNT(NAME)
FROM CITY
WHERE POPULATION > 100000
```

