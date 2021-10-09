---
title:  "[Basic Select] Weather Observation Station 5"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: 
toc_sticky: True

date: 2021-10-08
last_modified_at: 2021-10-09
---

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