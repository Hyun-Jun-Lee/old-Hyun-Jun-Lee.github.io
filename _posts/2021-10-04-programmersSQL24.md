---
title:  "[String, Date] 오랜 기간 보호한 동물(2) "
excerpt: "Level 2"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-04
last_modified_at: 2021-10-04
---

# [String, Date] 오랜 기간 보호한 동물(2)

> 문제

![image](https://user-images.githubusercontent.com/76996686/135845430-dadc8bcf-0ea8-471c-8db7-4ffa03076851.png)




<br>

> 답

```sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_INS AS I INNER JOIN ANIMAL_OUTS AS O
    ON I.ANIMAL_ID = O.ANIMAL_ID
ORDER BY I.DATETIME - O.DATETIME 
LIMIT 2
```
