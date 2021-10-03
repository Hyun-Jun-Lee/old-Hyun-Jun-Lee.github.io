---
title:  "[String, Date] 중성화 여부 파악하기 "
excerpt: "Level 2, CASE~WHEN"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-03
last_modified_at: 2021-10-03
---

# [String, Date] 중성화 여부 파악하기

> 문제

![image](https://user-images.githubusercontent.com/76996686/135758282-c0d08bc2-6a92-4b4c-996e-a9ead16416ac.png)



<br>

> 답

```sql
SELECT ANIMAL_ID, NAME,
    CASE
        WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR SEX_UPON_INTAKE LIKE 'Spayed%'
        THEN 'O'
        ELSE 'X'
        END AS '중성화'
FROM ANIMAL_INS
```

## CASE~WHEN

```SQL
SELECT *
    CASE
        WHEN : 조건문
        THEN : 참이면 실행할 부분
        ELSE : 거짓이면 실행할 부분
        END : IF 문 종료
```