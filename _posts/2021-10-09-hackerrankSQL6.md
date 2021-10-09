---
title:  "[Basic Select] Weather Observation Station 1~3"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: false
toc_sticky: false

date: 2021-10-08
last_modified_at: 2021-10-08
---

# [Basic Select] Weather Observation Station 1

> 문제

Query a list of CITY and STATE from the STATION table.


<br>

> 답

```sql
select city, state
from station
```


# [Basic Select] Weather Observation Station 3

> 문제

Query a list of CITY names from STATION for cities that have an even ID number. Print the results in any order, but exclude duplicates from the answer.

- STATION 테이블에서 ID number가 짝수인 City Name을 출력해라 + 중복 X
  - even number : 짝수 / odd number : 홀수

<br>

> 답

```sql
select distinct city 
from station
where (id%2)=0;
```
