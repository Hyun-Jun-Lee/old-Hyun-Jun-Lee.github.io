---
title:  "[GROUP BY] 동물 동명 수 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-19
last_modified_at: 2021-09-19
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133912400-62f09e7f-fb5b-464f-8b5b-37e00946b6da.png)



<br>

> 답

```sql
SELECT NAME, COUNT(NAME) AS cnt
FROM ANIMAL_INS
GROUP BY NAME -- 같은 이름 별로 먼저 그룹화를 해준다음
HAVING COUNT(NAME)>=2 -- 2회이상 쓰인 이름만
ORDER BY NAME
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