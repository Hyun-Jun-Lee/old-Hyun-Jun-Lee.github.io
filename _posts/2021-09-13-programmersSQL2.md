---
title:  "[SELECT] 역순 정렬하기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-13
last_modified_at: 2021-09-13
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133086428-9bbe105b-e884-4b7c-a56b-655b0003af8a.png)

<br>

> 답

```sql

SELECT NAME, DATETIME 
FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC -- desc : 내림차순

```