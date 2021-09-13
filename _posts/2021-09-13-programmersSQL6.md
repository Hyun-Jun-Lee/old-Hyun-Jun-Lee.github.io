---
title:  "[SELECT] 상위 n개 레코드 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-13
last_modified_at: 2021-09-13
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133094425-693fb4d2-029c-4e77-8c49-7f41ed1f69bf.png)



<br>

> 답

```sql
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME
LIMIT 1 -- python head와 비슷
```