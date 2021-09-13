---
title:  "[SELECT] 어린 동물 찾기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-13
last_modified_at: 2021-09-13
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133088180-b0f7ef0f-9b14-414d-a49b-efa03e41cbe5.png)



<br>

> 답

```sql

SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION != 'Aged'
ORDER BY ANIMAL_ID ASC -- order by default값이 asc

```