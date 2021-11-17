---
title:  "[advance Select] Occupations"
excerpt: "Difficulty : medium"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-17
last_modified_at: 2021-11-17
---

# [advance Select] Occupations

> 문제

각각의 이름을 알파벳순으로 정렬 후 직업(Occupation)을 보여주는데, 직업을 기준으로 Pivot 테이블로 변환<br>
이 때 변환한 Pivot 테이블의 칼럼명은 Doctor, Professor, Singer, Actor 순이다. (각 직업에 대응하는 이름이 없다면 NULL을 반환)

```
The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.
```

<br>

- pivot table

![image](https://user-images.githubusercontent.com/76996686/142149352-ea4b2cca-d000-4dd4-b918-44cd43e112fc.png)

<a href="https://techblog-history-younghunjo1.tistory.com/159">참고 블로그</a>

> 답

```sql
-- 각 직업별 Index를 세기 위한 변수 설정(각 직업별로 첫번째로 오는 name, 두번째로 오는 name 등을 알아내기 위해)
SET @D=0, @P=0, @S=0, @A=0;

-- 문자열의 알파벳순서에서 최솟값(MIN)은 A(a)로 시작하는 것을 추출해줌!
SELECT MIN(Doctor), MIN(Professor), MIN(Singer), MIN(Actor)
FROM (SELECT CASE WHEN Occupation = 'Doctor' THEN Name END AS Doctor,
             CASE WHEN Occupation = 'Professor' THEN Name END AS Professor,
             CASE WHEN Occupation = 'Singer' THEN Name END AS Singer,
             CASE WHEN Occupation = 'Actor' THEN Name END AS Actor,
             CASE
             WHEN Occupation = 'Doctor' THEN (@D:=@D+1)
             WHEN Occupation = 'Professor' THEN (@P:=@P+1)
             WHEN Occupation = 'Singer' THEN (@S:=@S+1)
             WHEN Occupation = 'Actor' THEN (@A:=@A+1)
             END AS RowNumber
       FROM Occupations
       ORDER BY Name) sub
GROUP BY RowNumber
```

