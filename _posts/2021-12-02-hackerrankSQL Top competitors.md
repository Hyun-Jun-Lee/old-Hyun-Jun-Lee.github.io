---
title:  "[Basic join] Top Competitors"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-30
last_modified_at: 2021-11-30
---

# [Basic join] Top Competitors

> 문제

Write a query to print the `respective hacker_id and name of hackers who achieved full scores for more than one challenge.` Order your output in `descending order by the total number of challenges in which the hacker earned a full score.` If more than one hacker received full scores in same number of challenges, `then sort them by ascending hacker_id.`

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
SELECT H.hacker_id, H.name
FROM Submissions s
    INNER JOIN Challenges c ON s.challenge_id = c.challenge_id
    INNER JOIN Difficulty d ON c.difficulty_level = d.difficulty_level
    INNER JOIN Hackers h ON s.hacker_id = h.hacker_id
WHERE S.score = D.score
GROUP BY s.hacker_id, h.name
HAVING count(s.challenge_id) > 1 -- who achieved full scores for more than one challenge / Full score count
ORDER BY count(s.challenge_id) DESC, s.hacker_id
```

