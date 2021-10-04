---
title:  "[String, Date] DATETIME에서 DATE로 형 변환"
excerpt: "Level 2"

categories:
- Programmers SQL

toc: false
toc_sticky: false

date: 2021-10-04
last_modified_at: 2021-10-04
---

# [String, Date] DATETIME에서 DATE로 형 변환

> 문제

![image](https://user-images.githubusercontent.com/76996686/135857559-0f8178dd-1464-4cf5-a53e-2b86bd4195a0.png)


<br>

> 답

```sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, "%Y-%m-%d") AS 날짜
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

- DATE_FORMAT은 날짜 포맷을 지정해주는 함수