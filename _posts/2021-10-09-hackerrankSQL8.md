---
title:  "[Basic Select] Weather Observation Station 6,7"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-08
last_modified_at: 2021-10-10
---

# [Basic Select] Weather Observation Station 6

> 문제

Query the list of CITY names starting with vowels (i.e., a, e, i, o, or u) from STATION. Your result cannot contain duplicates.

station 테이블 중 모음(i.e., a, e, i, o, or u)으로 시작하는 CITY name 구하라 + 중복 제외


<br>

> 답

```sql
-- 내 답
select distinct city
from station
where (city like 'a%' 
       or city like 'e%'
       or city like 'i%'
       or city like 'o%'
       or city like 'u%'
       )

-- 모법 답
select distinct city
from station
where left(city,1) in ('a','e','i','o','u')
```

# [Basic Select] Weather Observation Station 7

> 문제

Query the list of CITY names ending with vowels (a, e, i, o, u) from STATION. Your result cannot contain duplicates.

station 테이블 중 모음(i.e., a, e, i, o, or u)으로 끝나는 CITY name 구하라 + 중복 제외


<br>

> 답

```sql
-- 내 답
select distinct city
from station
where (city like 'a%' 
       or city like 'e%'
       or city like 'i%'
       or city like 'o%'
       or city like 'u%'
       )

-- 모법 답
select distinct city
from station
where right(city,1) in ('a','e','i','o','u') -- where REGEXP '[aeiou]$' -> 정규표현식 사용 가능
```

## 문자열 자르기 함수

- LEFT(컬럼명, 문자열 길이) : 왼쪽 부터 시작해서 컬럼을 문자열 길이 만큼 자름
- SUBSTRING(문자열,시작자리번호,자를문자수)
- 정규표현식 참고 링크(https://velog.io/@gillog/MySQL-REGEXPRegular-Expression%EC%A0%95%EA%B7%9C-%ED%91%9C%ED%98%84%EC%8B%9D)