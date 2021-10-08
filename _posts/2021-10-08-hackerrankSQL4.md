---
title:  "[Basic Select] Japanese Cities' Attributes"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: false
toc_sticky: false

date: 2021-10-08
last_modified_at: 2021-10-08
---

# [Basic Select] Japanese Cities' Attributes

> 문제

Query all attributes of every Japanese city in the CITY table. The COUNTRYCODE for Japan is JPN.

<br>

> 답

```sql
select *
from city
where countrycode = 'jpn'
```
