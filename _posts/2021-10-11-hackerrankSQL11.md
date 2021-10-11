---
title:  "[Basic Select] Weather Observation Station 10"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-11
last_modified_at: 2021-10-11
---

# [Basic Select] Weather Observation Station 10

> 문제

Query the list of CITY names from STATION that do not end with vowels. Your result cannot contain duplicates.



station 테이블 중 모음(i.e., a, e, i, o, or u)으로 끝나지 않는 CITY name 구하라 + 중복 제외


<br>

> 답

```sql
-- 내 답
select distinct city
from station
where city regexp '[^aeiou]$'
```

# 정규 표현식

## Matching

- `.` : 문자 하나, '...' = 문자열 길이가 세글자 이상인 것
- `|` : |로 구분된 문자에 해당하는 문자열 찾기, "A|B" = A또는 B에 해당하는 문자열 찾기
- `[]` : '[123]d' = 대상 문자열에서 1d or 2d, 3d인 문자열 찾기
- `^` : 시작하는 문자열 찾기
- `$` : 끝나는 문자열 찾기

## Numbers Limit

- `*` : 0회 이상 나타나는 문자, 'a*' = 'b', 'ab', 'aa' 등
- `+` : 1회 이상 나타나는 문자
- `{m,n}` : m회 이상 n회 이하 반복되는 문자, '치{1,2}' = '치'가 1회 이상 2회이하 반복하는 문자열 찾기
  
## String Group

- `[A-z]` : 알파벳 대문자or소문자 찾기, '[A-z]+' = 알파벳이 한개 이상인 문자열 찾기
- `[0-9]` : 숫자인 문자열 찾기, '^[0-9]+' = 한 개 이상의 숫자로 시작하는 문자열 찾기

## Not

- `[^문자]` : 괄호 안의 문자를 포함하지 않은 문자열 찾기