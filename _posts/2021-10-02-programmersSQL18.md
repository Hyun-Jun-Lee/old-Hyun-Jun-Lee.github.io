---
title:  "[JOIN]] 있었는데요 없었습니다 "
excerpt: "Level 3"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-02
last_modified_at: 2021-10-02
---

# [JOIN]] 있었는데요 없었습니다

> 문제

![image](https://user-images.githubusercontent.com/76996686/135719839-b73f879c-fbac-4384-958d-539ab48dbf5a.png)




<br>

> 답

```sql
SELECT O.ANIMAL_ID, O.NAME
FROM ANIMAL_INS AS I INNER JOIN ANIMAL_OUTS AS O
    ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.DATETIME > O.DATETIMEㅍ -- 입양일(I.DATETIME)이 보호일(O.DATETIME)보다 빠른 정보 찾아야함
ORDER BY I.DATETIME
```

- 입양일(I.DATETIME), 보호일(O.DATETIME) 정보 둘다 필요하므로 INNER JOIN


<br>

## JOIN

- 여러 테이블 한번에 검색하게 해주는 기능, 두 테이블이 공통으로 가지고 있는 열(외래키)가 있어야함

    - INNER JOIN : 교집합
    - OUTER JOIN : 합집합
      - LEFT JOIN : 왼쪽 테이블은 전체, 오른쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 오른쪽 테이블은 NULL 포함 가능)
      - RIGHT JOIN : 오른쪽 테이블은 전체, 왼쪽 테이블은 두 외래키 값이 같은 것만 리턴(즉, 왼쪽 테이블은 NULL 포함 가능)