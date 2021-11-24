---
title:  "[advance Select] Type of Triangle"
excerpt: "Difficulty : easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-24
---

# [advance Select] Type of Triangle

> 문제

삼각형의 타입을 판별하는 쿼리를 작성

Equilateral(정삼각형): 세변의 길이가 같은 삼각형
Isosceles(이등변 삼각형): 두변의 길이가 같은 삼각형
Scalene: 3변의 길이가 다른 삼각형
Not A Triangle: 삼각형이 아님

<br>

- pivot table

![image](https://user-images.githubusercontent.com/76996686/142149352-ea4b2cca-d000-4dd4-b918-44cd43e112fc.png)

<a href="https://techblog-history-younghunjo1.tistory.com/159">참고 블로그</a>

> 답

```sql
SELECT 
CASE
    WHEN A = B AND B = C THEN "Equilateral"
    WHEN A + B <= C THEN "Not A Triangle"
    WHEN A != B AND B != C AND A != C THEN "Scalene"
    ELSE "Isosceles"
END AS A
FROM TRIANGLES
```

