---
title:  "[Basic join] The Blunder"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] The Blunder

> 문제

Samantha was tasked with `calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 0 key was broken until after completing the calculation.` She wants your help finding the `difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.`

Write a query `calculating the amount of error (i.e.: actual-miscalculated average monthly salaries), and round it up to the next integer.`

<br>

> Note

- CEIL(숫자) : 올림
- ROUND(숫자, 자릿수) : 반올림
- TRUNCATE(숫자, 자릿수) : 내림
- FLOOR(숫자) : 소숫점 아래 버림
- ABS(숫자) : 절대값
- POW(x,y) : x의 y 승
- MOD(x,y) : x를 y로 나눈 나머지

> 답

```sql
SELECT CEIL(AVG(Salary) - AVG(REPLACE(Salary, 0, '')))
FROM EMPLOYEES
```

