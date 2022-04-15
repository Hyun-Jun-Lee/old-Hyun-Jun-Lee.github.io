---
title:  "[sort] 10989번 수 정렬하기 3"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-04-16
last_modified_at: 2022-04-16
---

# [sort] 10989번 수 정렬하기 3

> 문제

N개의 수가 주어졌을 때, 이를 오름차순으로 정렬하는 프로그램을 작성하시오.

메모리제한 8MB


> 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 10,000,000)이 주어진다. 둘째 줄부터 N개의 줄에는 수가 주어진다. 이 수는 10,000보다 작거나 같은 자연수이다.


> 출력

첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 한 줄에 하나씩 출력한다.

> 예제 입력

```
10
5
2
3
1
4
2
3
5
1
7
```

> 예제 출력

'''
1
1
2
2
3
3
4
5
5
7
'''

<br>

> 풀이

```python
import sys

n = int(input())
check = [0] * 10001

for _ in range(n):
    num = int(sys.stdin.readline())
    check[num] += 1

for i in range(10001):
    if check[i] != 0:
        for _ in range(check[i]):
            print(i)
```

- n이 10,000 보다 작거나 같은 수 라고 미리 주어졌고 메모리가 제한되어 있으므로 list 길이를 `check = [0] * 10001`로 미리 지정


```python
for _ in range(n):
    num = int(sys.stdin.readline())
    check[num] += 1
```

n만큼 반복하면서 num을 입력 받고, `check` 리스트의 num번째 인덱스 value를 +1 씩 누적
(ex. 5가 두번 나오면 `check[5] = 2` 가 됨)

```python
for i in range(10001):
    if check[i] != 0:
        for _ in range(check[i]):
            print(i)
```

10001 까지 i를 반복해주면서 value가 0이 아닌 경우들에 대해서 `check[i]` 만큼 반복하며 해당 i 출력
(ex. `check[5]`는 value가 2, 그래서 5가 두번 print 된다.)