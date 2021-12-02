---
title:  "[Basic join] Ollivander's Inventory"
excerpt: "Difficulty : Easy"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-12-02
last_modified_at: 2021-12-02
---

# [Basic join] Ollivander's Inventory

> 문제

Harry Potter and his friends are at Ollivander's with Ron, finally replacing Charlie's old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons `needed to buy each non-evil wand of high power and age.` Write a query to print the `id, age, coins_needed, and power of the wands` that Ron's interested in, sorted in order of `descending power.` If more than one wand has same power, sort the result in order of `descending age.`

<br>

> 답

```sql
SELECT w.ID, P.AGE, m.coins_needed, w.power 
from (SELECT code, min(coins_needed) as coins_needed, power 
      from wands 
      group by code, power) as m 
      inner join wands as w on w.code = m.code and w.power = m.power and w.coins_needed = m.coins_needed 
      inner join wands_property as p on p.code = w.code 
where p.is_evil = 0 
order by w.power desc, p.age desc
```

