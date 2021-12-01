---
title:  "[Basic join] Weather Observation Station 20"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-30
last_modified_at: 2021-11-30
---

# [Basic join] Weather Observation Station 20

> 문제



<br>

> Note

- CEIL(숫자) : 올림
- ROUND(숫자, 자릿수) : 반올림
- TRUNCATE(숫자, 자릿수) : 내림
- FLOOR(숫자) : 소숫점 아래 버림
- ABS(숫자) : 절대값
- POW(x,y) : x의 y 승
- MOD(x,y) : x를 y로 나눈 나머지

> 답

```sql
SET @rowIndex=-1;
SELECT ROUND(AVG(lat_n), 4) AS Median
FROM (SELECT @rowIndex:=@rowIndex+1 AS RowNumber,
                lat_n
      FROM station
      ORDER BY lat_n) sub
WHERE RowNumber IN (FLOOR(@rowIndex / 2), CEIL(@rowIndex / 2))
```

