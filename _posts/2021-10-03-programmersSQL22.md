---
title:  "[String, Date] 이름이 el이 들어가는 동물 찾기 "
excerpt: "Level 2"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-03
last_modified_at: 2021-10-03
---

# [String, Date] 이름이 el이 들어가는 동물 찾기

> 문제

![image](https://user-images.githubusercontent.com/76996686/135757295-7566a9e8-136c-4339-9031-7c42b818d55c.png)


<br>

> 답

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE NAME LIKE '%el%' AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME 
```
