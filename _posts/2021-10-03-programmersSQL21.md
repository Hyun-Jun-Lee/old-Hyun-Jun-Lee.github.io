---
title:  "[String, Date] 루시와 엘라 찾기 "
excerpt: "Level 2"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-03
last_modified_at: 2021-10-03
---

# [String, Date] 루시와 엘라 찾기

> 문제

![image](https://user-images.githubusercontent.com/76996686/135756320-c850c10b-9435-4a50-9306-ca36370b721c.png)



<br>

> 답

```sql
SELECT ANIMAL_ID,NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy','Ella','Pickle','Rogan','Sabrina','Mitty')
```
