---
title:  "[JOIN]] 오랜기간 보호한 동물 1 "
excerpt: "Level 3"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-03
last_modified_at: 2021-10-03
---

# [JOIN]] 오랜기간 보호한 동물 1

> 문제

![image](https://user-images.githubusercontent.com/76996686/135751765-e959e829-75f5-48f9-a7f3-651db21f05e0.png)





<br>

> 답

```sql
SELECT I.NAME, I.DATETIME
FROM ANIMAL_INS AS I LEFT JOIN ANIMAL_OUTS AS O
    ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE O.ANIMAL_ID IS NULL -- 입양 테이블에 없는 I.ANIMAL_ID 만 조회(= 아직 입양을 못간 동물)
ORDER BY I.DATETIME 
LIMIT 3
```

- 입양 테이블엔 기록이 없지만 보호소 테이블엔 기록이 있어야하니 LEFT JOIN


<br>

## JOIN

- 여러 테이블 한번에 검색하게 해주는 기능, 두 테이블이 공통으로 가지고 있는 열(외래키)가 있어야함

    - INNER JOIN : 교집합
    - OUTER JOIN : 합집합
      - LEFT JOIN : 왼쪽 테이블은 전체, 오른쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 오른쪽 테이블은 NULL 포함 가능)
      - RIGHT JOIN : 오른쪽 테이블은 전체, 왼쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 왼쪽 테이블은 NULL 포함 가능)