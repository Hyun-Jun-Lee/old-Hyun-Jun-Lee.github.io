---
title:  "[JOIN]] 없어진 기록 찾기 "
excerpt: "Level 3"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-02
last_modified_at: 2021-10-02
---

# [JOIN]] 없어진 기록 찾기

> 문제

![image](https://user-images.githubusercontent.com/76996686/135717692-02907ac4-72d6-4ae6-8f95-762a355a9bab.png)



<br>

> 답

```sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_INS AS I RIGHT JOIN ANIMAL_OUTS AS O 
    ON I.ANIMAL_ID = O.ANIMAL_ID -- ANIMAL_ID 기준으로 join
WHERE I.ANIMAL_ID IS NULL -- ANIAML_INS 테이블에 없는 ID는 유실된 정보
ORDER BY O.ANIMAL_ID
```

<br>

## JOIN

- 여러 테이블 한번에 검색하게 해주는 기능, 두 테이블이 공통으로 가지고 있는 열(외래키)가 있어야함

    - INNER JOIN : 교집합
    - OUTER JOIN : 합집합
      - LEFT JOIN : 왼쪽 테이블은 전체, 오른쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 오른쪽 테이블은 NULL 포함 가능)
      - RIGHT JOIN : 오른쪽 테이블은 전체, 왼쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 왼쪽 테이블은 NULL 포함 가능)