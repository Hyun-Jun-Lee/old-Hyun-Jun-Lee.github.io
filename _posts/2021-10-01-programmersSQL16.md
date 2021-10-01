---
title:  "[Null] Null 처리하기 "
excerpt: "Null 처리 함수"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-01
last_modified_at: 2021-10-01
---

# [Null] Null 처리하기

> 문제

![image](https://user-images.githubusercontent.com/76996686/135614184-ecfd02d1-0bd1-4e40-8603-5662ab60079c.png)


<br>

> 답

```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, "No name"), SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

<br>

## NULL 처리 함수

- IFNULL() (oracle에선 NVL)
```sql
SELECT IFNULL(column명, "null일 경우 대체 값") FROM 테이블명;
```

- IF() 이용한 처리
```sql
-- NAME Column이 NULL이 True인 경우 "No name"을, False인 경우는 NAME Column을 출력
SELECT IF(IS NULL(NAME), "No name", NAME) FROM 테이블명;
```

- CASE
  - 해당 column 값을 조건식을 통해 True, False 판단해서 조건에 맞게 Column 값을 변환할 때 사용

```sql
CASE 
    WHEN 조건식1 THEN 식1
    WHEN 조건식2 THEN 식2
    ...
    ELSE 조건에 맞는경우가 없는 경우 실행할 식
END
```

- Example
```sql
SELECT 
    CASE
        WHEN NAME IS NULL THEN "No name"
        ELSE NAME
    END
FROM ANIMAL_INS
```