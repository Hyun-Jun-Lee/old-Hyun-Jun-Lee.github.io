---
title:  "[Basic join] Top Earnersr"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-25
last_modified_at: 2021-11-25
---

# [Basic join] Top Earnersr

> 문제

We define an employee's total earnings to be their monthly 'salary x months' worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to `find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings.` Then print these values as 2 space-separated integers.

<br>


> 답

```sql
SELECT salary * months as earnings, COUNT(*) -- COUNT(earnings)는 아직 없는 column이라 안되는듯
FROM Employee
GROUP BY earnings
ORDER BY earnings DESC
LIMIT 1
```

