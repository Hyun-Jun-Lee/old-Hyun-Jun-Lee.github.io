---
title:  "[SUM, MAX, MIN] 최대값 구하기 "
excerpt: "Programmers SQL "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-18
last_modified_at: 2021-09-18
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133863581-48e4f87e-5b90-45f7-8216-0a7209f293fc.png)



<br>

> 답

```sql
SELECT DATETIME
FROM ANIMAL_INS
ORDER BY DATETIME DESC
LIMIT 1
```