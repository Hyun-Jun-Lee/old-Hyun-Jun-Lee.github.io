---
title:  "[서브쿼리, 변수] 입양 시각 구하기2 "
excerpt: "Programmers SQL Level4 "

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-09-19
last_modified_at: 2021-09-19
---

> 문제

![image](https://user-images.githubusercontent.com/76996686/133914075-f9e5d88e-d368-4ca8-aed0-4891e65ce5ff.png)



<br>

> 답

```sql
SET @hour := -1; -- 변수명과 초기값 설정
SELECT (@hour := @hour +1) as HOUR, -- @hour의 값에 1씩 증가시키며 SELECT 전체 실행
    (SELECT COUNT(*)
    FROM ANIMAL_OUTS
    WHERE HOUR(DATETIME) = @hour)
FROM ANIMAL_OUTS
WHERE @hour < 23
```

<br>

> 변수

- @가 붙은 변수는 프로시저가 종료되어도 유지(0부터23까지)
- `:=`는 비교 연산자 `=`과 구별하기 위한 대입 연산자

