---
title:  "[Basic Select] Japanese Cities' Names"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: false
toc_sticky: false

date: 2021-10-08
last_modified_at: 2021-10-08
---

# [Basic Select] Japanese Cities' Names

> 문제

Query the names of all the Japanese cities in the CITY table. The COUNTRYCODE for Japan is JPN.


<br>

> 답

```sql
select name
from city
where countrycode = 'jpn'
```
