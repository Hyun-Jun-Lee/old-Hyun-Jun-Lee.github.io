---
title:  "[Basic Select] Employee Names"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-18
last_modified_at: 2021-10-18
---

# [Basic Select] Employee Names

> 문제

Write a query that prints a list of employee names (i.e.: the name attribute) from the Employee table in alphabetical order.


Employee 테이블에서 employee 이름을 조회하라 + 알파벳 순서로 정렬


<br>

> 답

```sql
-- 내 답
SELECT name
FROM Employee
ORDER BY name asc
```