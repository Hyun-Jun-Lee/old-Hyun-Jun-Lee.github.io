---
title:  "[1차원배열] 2562번 최댓값"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2021-12-30
last_modified_at: 2021-12-30
---

# [1차원배열] 2562번 최댓값

> 문제

9개의 서로 다른 자연수가 주어질 때, 이들 중 최댓값을 찾고 그 최댓값이 몇 번째 수인지를 구하는 프로그램을 작성하시오.

예를 들어, 서로 다른 9개의 자연수

3, 29, 38, 12, 57, 74, 40, 85, 61

이 주어지면, 이들 중 최댓값은 85이고, 이 값은 8번째 수이다.


> 입력

첫째 줄부터 아홉 번째 줄까지 한 줄에 하나의 자연수가 주어진다. 주어지는 자연수는 100 보다 작다.

> 출력

첫째 줄에 최댓값을 출력하고, 둘째 줄에 최댓값이 몇 번째 수인지를 출력한다.

<br>

> 풀이

```python
n = []

# list comprehension
# n = [int(input()) for _ in range(9)]

for i in range(9):
    a = int(input())
    n.append(a)

print(max(n))
# 0부터 시작하므로 +1
print(n.index(max(n))+1)
```