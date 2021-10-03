---
title:  "[JOIN] 보호소에서 중성화한 동물 "
excerpt: "Level 4, LIKE 연산자"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-03
last_modified_at: 2021-10-03
---

# [JOIN] 보호소에서 중성화한 동물

> 문제

![image](https://user-images.githubusercontent.com/76996686/135752974-d367bebe-da5f-40aa-bb7f-16b02d2e47a4.png)



<br>

> 답

```sql
SELECT I.ANIMAL_ID, I.ANIMAL_TYPE, I.NAME
FROM ANIMAL_INS AS I LEFT JOIN ANIMAL_OUTS AS O
    ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.SEX_UPON_INTAKE LIKE '%intact%'
    AND O.SEX_UPON_OUTCOME NOT LIKE '%intact%'
ORDER BY I.ANIMAL_ID
```

<br>

## LIKE

- 특정 값이 들어간 값을 검색할 때 사용 (반대는 NOT LIKE)

    - LIKE "VALUE" : VALUE라는 row만 출력
    - LIKE "%VALUE" : 뒤가 VALUE로 끝나는 값. 
    - LIKE "VALUE%" : VALUE로 시작하는 값. 
    - LIKE "%VALUE%" : VALUE가 들어가는 값.
    - LIKE "_VALUE" : 첫번째 글자 뒤에 VALUE가 들어가는 값
    - LIKE "__VALUE%" : 두번째 글자 뒤에 VALUE가 들어가는 값(뒤에는 어떤 글자 오던 상관 x)

