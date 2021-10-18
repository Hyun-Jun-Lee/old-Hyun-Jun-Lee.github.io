---
title:  "[Basic Select] Employee Salaries"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-18
last_modified_at: 2021-10-18
---

# [Basic Select] Employee Salaries

> 문제

Write a query that prints a list of employee names (i.e.: the name attribute) for employees in Employee having a salary greater than `2000` per month who have been employees for less than `10` months. Sort your result by ascending employee_id.


Employee 테이블에서 연봉이 2000 보다 높고 10개월 미만으로 일한 employee 이름을 조회하라 + ID순으로 정렬


<br>

> 답

```sql
SELECT name
FROM Employee
WHERE salary > 2000 and months <10
ORDER BY employee_id
```