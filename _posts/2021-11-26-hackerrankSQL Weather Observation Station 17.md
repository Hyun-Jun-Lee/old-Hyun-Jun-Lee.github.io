---
title:  "[Basic join] Weather Observation Station 17"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-26
last_modified_at: 2021-11-26
---

# [Basic join] Weather Observation Station 17

> 문제

Query the Western Longitude (LONG_W)where the smallest Northern Latitude (LAT_N) in STATION is greater than 38.7780. Round your answer to  decimal places.

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
SELECT ROUND(LONG_W,4)
FROM STATION
WHERE LAT_N > '38.7880'
ORDER BY LAT_N ASC
LIMIT 1
```

