---
title:  "[GROUP BY] 입양 시각 구하기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-19
last_modified_at: 2021-09-19
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133913656-8f715343-9055-4fdf-9abb-ffd67118857c.png)


<br>

> 답

```sql
SELECT HOUR(DATETIME), COUNT(*)
FROM ANIMAL_OUTS
WHERE HOUR(DATETIME) >=9 and HOUR(DATETIME)<20
GROUP BY HOUR(DATETIME)
ORDER BY hOUR(DATETIME)
```

<br>

> datetime

- YEAR : 연도 추출
- MONTH : 월 추출
- DAY : 일 추출 (DAYOFMONTH와 같은 함수)
- HOUR : 시 추출
- MINUTE : 분 추출
- SECOND : 초 추출

