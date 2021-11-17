---
title:  "[advance Select] new company"
excerpt: "Difficulty : medium"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-11-17
last_modified_at: 2021-11-17
---

# [advance Select] new company

> 문제

write a query to print the company_code, founder name, total number of lead managers, total number of senior managers, total number of managers, and total number of employees. Order your output by ascending company_code.

Company의 Company_code / Founder / 각 회사의 Lead Manager, Senior Manager, Manager, Employee 명수를 출력<br>
데이터 정렬 기준은 Company의 Company_code 기준으로 오름차순 정렬하는데, Company_code값이 문자열 형태이기 때문에 값에 숫자가 들어있더라도 문자열 취급

<br>

> 내 풀이

```sql
SELECT c.company_code, c.founder,
       COUNT(DISTINCT(l.lead_manager_code)), COUNT(DISTINCT(s.senior_manager_code)),
       COUNT(DISTINCT(m.manager_code)), COUNT(DISTINCT(e.employee_code))
FROM 
    company AS c INNER JOIN lead_manager AS l ON c.company_code = l.lead_manager
    senior_manager AS s INNER JOIN l ON s.lead_manager_code = l.lead_manager_code
    manager AS m INNER JOIN s ON m.senior_manager_code = s.senior_manager_code
    employee AS e INNER JOIN m ON m.manager_code = e.manager_code
ORDER BY c.company_code
```

<br>

> 답

```sql

SELECT c.company_code, c.founder,
       COUNT(DISTINCT(l.lead_manager_code)), COUNT(DISTINCT(s.senior_manager_code)),
       COUNT(DISTINCT(m.manager_code)), COUNT(DISTINCT(e.employee_code))
FROM company AS c, lead_manager AS l, senior_manager AS s, manager AS m, employee AS e
WHERE c.company_code = l.company_code AND
      l.lead_manager_code = s.lead_manager_code AND
      s.senior_manager_code = m.senior_manager_code AND
      m.manager_code = e.manager_code
GROUP BY c.company_code, c.founder 
ORDER BY c.company_code
```

