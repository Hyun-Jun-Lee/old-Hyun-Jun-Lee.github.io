---
title:  "[Basic Select] Higher Than 75 Marks"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-18
last_modified_at: 2021-10-18
---

# [Basic Select] Higher Than 75 Marks

> 문제

Query the Name of any student in STUDENTS who scored higher than `75` Marks. Order your output by the last three characters of each name. If two or more students both have names ending in the same last three characters (i.e.: Bobby, Robby, etc.), secondary sort them by ascending ID.


STUDENTS 테이블에서 Mark가 75 이상인 학생을 조회하고 결과를 각 이름의 마지막 3글자에 따라 정렬 + 두번쨰 정렬조건은 ID 오름차순


<br>

> 답

```sql
-- 내 답
SELECT Name
FROM STUDENTS
WHERE Marks > 75
ORDER BY RIGHT(NAME,3), ID ASC
```