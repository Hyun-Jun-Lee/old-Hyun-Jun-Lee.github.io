---
title:  "[Basic Select] Revising the Select Query II"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: false
toc_sticky: false

date: 2021-10-08
last_modified_at: 2021-10-08
---

# [Basic Select] Revising the Select Query II

> 문제

Query the NAME field for all American cities in the CITY table with populations larger than 120000. The CountryCode for America is USA.


<br>

> 답

```sql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'USA' AND POPULATION > 120000
```
