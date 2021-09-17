---
title:  "[SUM, MAX, MIN] 최소값 구하기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-18
last_modified_at: 2021-09-18
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133864006-69fa7648-9150-4f68-bf07-b246af2828b0.png)



<br>

> 답

```sql
SELECT DATETIME
FROM ANIMAL_INS
ORDER BY DATETIME ASC
LIMIT 1
```