---
title:  "[Basic join] The Report"
excerpt: "Difficulty : Medium"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-24
last_modified_at: 2021-11-25
---

# [Basic join] The Report

> 문제

Ketty doesn't want the `NAMES of those students who received a grade lower than 8.` 
The report must be in `descending order by grade -- i.e. higher grades are entered first.`
If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their `name alphabetically. `
Finally, `if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order`. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

<br>

> 답

```sql
SELECT IF(G.Grade<8,NULL,S.NAME) -- IF(조건, True, False)
    ,G.Grade, S.Marks
-- Between 사용하여 join
FROM Students as S INNER JOIN Grades as G ON (S.Marks BETWEEN G.Min_Mark AND G.Max_Mark)
ORDER BY G.GRADE DESC, S.NAME
```

