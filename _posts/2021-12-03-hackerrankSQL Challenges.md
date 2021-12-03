---
title:  "[Basic join] Challenges"
excerpt: "Difficulty : Medium"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-12-03
last_modified_at: 2021-12-03
---

# [Basic join] Challenges

> 문제

Julia asked her students to create some coding challenges. `Write a query to print the hacker_id, name, and the total number of challenges created by each student.` Sort your results by the `total number of challenges in descending order.` If more than one student created the same number of challenges, then sort the result by hacker_id. If more than one student created the same number of challenges and the count is less than the maximum number of challenges created, then exclude those students from the result.

<br>

- 각 학생의 hacker_id, name, 문제를 만든 총 개수를 출력
- 정렬은 총 문제 개수의 내림차순으로 한다. 만약 똑같은 문제 개수를 만든 학생이 2명 이상이라면, 그 때는 hacker_id 를 기준으로 오름차순으로 정렬
-  2명 이상이 똑같은 문제 개수를 만들었을 때, 그 문제 개수가 문제 개수의 최댓값보다 작다면 그 때의 학생들은 출력시키지 않아야 한다

> 답

- https://techblog-history-younghunjo1.tistory.com/157

```sql
SELECT Hackers.hacker_id, Hackers.name, COUNT(*) AS challenges_created
FROM Hackers
 INNER JOIN Challenges ON Hackers.hacker_id = Challenges.hacker_id
GROUP BY Hackers.hacker_id, Hackers.name
-- challenges_created 값이 2개 이상 중복되지 않고 1개인 값들
HAVING challenges_created IN (SELECT sub2.challenges_created
                              FROM (SELECT hacker_id, COUNT(*) AS challenges_created
                                    FROM Challenges
                                    GROUP BY Challenges.hacker_id) sub2
                              GROUP BY sub2.challenges_created
                              HAVING COUNT(*) = 1)
-- challenges_created 최대 값
    OR challenges_created = (SELECT MAX(sub1.challenges_created)
                             FROM (SELECT COUNT(*) AS challenges_created
                                   FROM Challenges
                                   GROUP BY Challenges.hacker_id) sub1)
ORDER BY challenges_created DESC, Hackers.hacker_id
```

