---
title:  "[Basic Select] Weather Observation Station 1~4"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: 
toc_sticky: True

date: 2021-10-08
last_modified_at: 2021-10-09
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

<br>

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

<br>

# [Basic Select] Weather Observation Station 4

> 문제

Find the difference between the total number of CITY entries in the table and the number of distinct CITY entries in the table.

For example, if there are three records in the table with CITY values 'New York', 'New York', 'Bengalaru', there are 2 different city names: 'New York' and 'Bengalaru'. The query returns 

- 전체 데이터 수 - 중복되지 않은 city name 구하기

<br>

> 답

```sql
select count(city) - count(distinct city)
from station
```

<br>

# [Basic Select] Weather Observation Station 5

> 문제

Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically. 

- You can write two separate queries to get the desired output. It need not be a single query.

station 테이블 중 도시의 이름과 도시의 이름의 길이를 출력하는데, 도시의 이름의 길이가 가장 짧은 도시의 이름과, 가장 긴 이름의 도시를 출력
만약 가장 짧은 도시의 이름이나, 가장 긴 이름의 도시가 복수로 있는 경우에는 알파벳 순서 중 가장 앞에 있는 것을 출력

    - 문자열 길이 함수 LENGTH(), CHAR_LENGTH()

<br>

> 답

```sql
SELECT CITY, LENGTH(CITY) AS LEN
FROM STATION
ORDER BY LEN, CITY
LIMIT 1;

SELECT CITY, LENGTH(CITY) AS LEN
FROM STATION
ORDER BY LEN DESC, CITY 
LIMIT 1;
```