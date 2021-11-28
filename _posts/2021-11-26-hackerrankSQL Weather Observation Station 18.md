---
title:  "[Basic join] Weather Observation Station 18"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-26
last_modified_at: 2021-11-28
---

# [Basic join] Weather Observation Station 18

> 문제

P1(a, b), P2(c, d)가 각각의 좌표
a에는 lat_n의 최솟값, b에는 long_w의 최솟값

c에는 lat_n의 최댓값, d에는 long_w의 최댓값

P1과 P2 좌표 사이의  Manhattan Distance

Manhattan Distance = | a - c | + | b - d |

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
SELECT ROUND(ABS(MIN(LAT_N)-MAX(LAT_N)) + ABS(MIN(LONG_W)-MAX(LONG_W)) ,4)
FROM STATION
```

