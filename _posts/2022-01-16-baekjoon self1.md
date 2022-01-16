---
title:  "[재귀] 10872번 팩토리얼"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-16
last_modified_at: 2022-01-16
---

# [재귀] 10872번 팩토리얼

> 문제

0보카 크거나 같은 정수 n이 주어진다. n!을 출력하는 프로그램을 작성하세요

> 입력

첫째 줄에 정수 N(0 ≤ N ≤ 12)이 주어진다.

> 출력

첫째 줄에 N!을 출력한다.

> 예제 입력

10

> 예제 출력

3628800

<br>

> 풀이

```python
n = int(input())

def facto(n):
    if n==0:
        return 1
    elif n==1:
        return 1
    
    return n * facto(n-1)

print(facto(n))
```
