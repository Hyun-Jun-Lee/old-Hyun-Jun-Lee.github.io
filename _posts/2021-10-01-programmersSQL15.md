---
title:  "[Null] 이름 없는/있는 동물의 ID "
excerpt: "Programmers SQL"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-01
last_modified_at: 2021-10-01
---

# 이름이 없는 동물 ID

> 문제

![image](https://user-images.githubusercontent.com/76996686/135611529-835d9fb1-bef5-4141-98f2-462e7c9a7c45.png)


<br>

> 답

```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME is NULL
```

<br>

# 이름이 있는 동물 ID

> 문제

![image](https://user-images.githubusercontent.com/76996686/135611988-03f8a8b4-8902-4ad0-a5d2-820e53856948.png)

> 답
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
```
