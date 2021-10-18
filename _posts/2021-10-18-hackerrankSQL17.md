---
title:  "[Basic Select] Binary Tree Nodes"
excerpt: "Difficulty : medium"

categories:
- HackerRank SQL

toc: True
toc_sticky: True

date: 2021-10-18
last_modified_at: 2021-10-18
---

# [Basic Select] Binary Tree Nodes

> 문제

You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.

Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:



각 노드가 어떤 노드를 가리키는지 문자열로 명시하고 출력 결과를 노드의 값 기준으로 오름차순하여 정렬해라. 이 때 루트노드라면 Root를, 가장 마지막의 노드들이라면 Leaf를, Root노드를 제외한 나머지 부모노드들은 Inner를 출력해라

<br>

- 2진 트리 문제. N은 이진 트리의 노드 값, P는 N의 상위 항목
  - Root → 최상위 노드인 경우, 부모가 없는 노드 → 5가 최상위 노드
  - Leaf → 최하위 노드인 경우, 자식이 없음 → 1, 3, 6, 9 → n이 p의 범위에 포함되지 않는 것들
  - Inner → root도 leaf도 아닌 경우 → 2, 8


> 답

```sql
-- Subquery
SELECT  N, 
    CASE WHEN P IS NULL THEN 'Root' -- parent가 null 일 때 Root node
    WHEN N NOT IN (SElECT Distinct P FROM bst WHERE P IS NOT NULL) THEN 'Leaf' -- parent 리스트 안에 N이 없을경우 Leaf node
    ELSE 'Inner' END
FROM BST
ORDER BY N
```

