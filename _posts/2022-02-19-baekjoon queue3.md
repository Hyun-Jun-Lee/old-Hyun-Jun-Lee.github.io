---
title:  "[Queue] 11866번 요세푸스 문제 0"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-02-19
last_modified_at: 2022-02-19
---

# [Queue] 11866번 요세푸스 문제 0

> 문제

요세푸스 문제는 다음과 같다.

1번부터 N번까지 N명의 사람이 원을 이루면서 앉아있고, 양의 정수 K(≤ N)가 주어진다. 이제 순서대로 K번째 사람을 제거한다. 한 사람이 제거되면 남은 사람들로 이루어진 원을 따라 이 과정을 계속해 나간다. 이 과정은 N명의 사람이 모두 제거될 때까지 계속된다. 원에서 사람들이 제거되는 순서를 (N, K)-요세푸스 순열이라고 한다. 예를 들어 (7, 3)-요세푸스 순열은 <3, 6, 2, 7, 5, 1, 4>이다.

N과 K가 주어지면 (N, K)-요세푸스 순열을 구하는 프로그램을 작성하시오.


> 입력

첫째 줄에 N과 K가 빈 칸을 사이에 두고 순서대로 주어진다. (1 ≤ K ≤ N ≤ 1,000)


> 출력

예제와 같이 요세푸스 순열을 출력한다.


> 예제 입력

```
7 3
```

> 예제 출력

'''
<3, 6, 2, 7, 5, 1, 4>
'''

<br>

> 풀이

```python
import sys
from collections import deque

n, k = map(int,sys.stdin.readline().split())
q = deque()

for i in range(1,n+1):
    q.append(i)
print('<', end='')

while q:
    # k-1번째 앞에 요소를 뒤로보냄
    for _ in range(k-1):
        q.append(q.popleft())
        # k번째 요소 빼기
    print(q.popleft(), end="")
    # 숫자 뒤에 , 출력하기 위한 코드
    if q:
        print(", ", end="")

print(">")
```

- `k-1` 번까지 요소들을 맨 뒤로 보낸뒤 k번째를 출력하면 된다.

