---
title:  "[GROUP BY] 고양이와 개는 몇마리 있을까 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-19
last_modified_at: 2021-09-19
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133912009-fc7038ce-ff78-4a20-9b04-8a66ba119518.png)



<br>

> 답

```sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_TYPE) AS cnt
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ('Dog','Cat')
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAl_TYPE 
```

<br>

> SQL 문 실행 순서

```sql
FROM
WHERE
GROUP BY
SELECT
ORDER BY
LIMIT
```

<br>

> WHERE VS HABING

- WHERE 
  - 전체 테이블 대상
  - 집계함수(COUNT, MAX, MIN, AVG, SUM) 사용 불가

- HAVING
  - GROUP BY 한 테이블 대상
  - 집계함수(COUNT, MAX, MIN, AVG, SUM) 사용 가능
  - SELECT 문에 `집계함수 사용 시 GROUP BY 사용 해야함`