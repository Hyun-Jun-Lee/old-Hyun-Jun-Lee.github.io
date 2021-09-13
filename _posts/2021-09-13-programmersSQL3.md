---
title:  "[SELECT] 아픈 동물 찾기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-13
last_modified_at: 2021-09-13
---

> 문제


<br>

> 답

```sql

SELECT NAME, DATETIME 
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC -- desc : 내림차순

```