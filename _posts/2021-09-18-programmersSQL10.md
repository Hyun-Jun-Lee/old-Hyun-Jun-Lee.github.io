---
title:  "[SUM, MAX, MIN] 중복 제거하기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-18
last_modified_at: 2021-09-18
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133864505-91829036-d35f-4ed7-bb8c-2d208d0bad7a.png)



<br>

> 답

```sql
SELECT COUNT(DISTINCT NAME)
FROM ANIMAL_INS
```

- 중복이 제거 된 NAME을 COUNT 해야하기 때문에 DISTINCT가 먼저 실행