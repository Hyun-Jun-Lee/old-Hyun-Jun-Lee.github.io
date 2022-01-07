---
title:  "[함수] 15596번 정수 N개의 합"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-07
last_modified_at: 2022-01-07
---

# [함수] 15596번 정수 N개의 합

> 문제

정수 n개가 주어졌을 때, n개의 합을 구하는 함수를 작성하시오.

작성해야 하는 함수는 다음과 같다.

a: 합을 구해야 하는 정수 n개가 저장되어 있는 리스트 (0 ≤ a[i] ≤ 1,000,000, 1 ≤ n ≤ 3,000,000)
리턴값: a에 포함되어 있는 정수 n개의 합 (정수)



<br>

> 풀이

```python
def sum_list(a):
    res = 0
    for i in a:
        res += i
    return res
```
