---
title:  "[수학] 2869번 달팽이는 올라가고 싶다"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-13
last_modified_at: 2022-01-13
---

# [수학] 2869번 달팽이는 올라가고 싶다

> 문제

땅 위에 달팽이가 있다. 이 달팽이는 높이가 V미터인 나무 막대를 올라갈 것이다.

달팽이는 낮에 A미터 올라갈 수 있다. 하지만, 밤에 잠을 자는 동안 B미터 미끄러진다. 또, 정상에 올라간 후에는 미끄러지지 않는다.

달팽이가 나무 막대를 모두 올라가려면, 며칠이 걸리는지 구하는 프로그램을 작성하시오.

> 입력

첫째 줄에 세 정수 A, B, V가 공백으로 구분되어서 주어진다. (1 ≤ B < A ≤ V ≤ 1,000,000,000)

> 출력

첫째 줄에 달팽이가 나무 막대를 모두 올라가는데 며칠이 걸리는지 출력한다.

> 예제 입력

2 1 5

> 예제 출력

4

<br>

> 풀이

```python
import math

a, b, v = map(int, input().split())

day = math.ceil((v-b)/(a-b))
print(day)
```

> 나무 정상에 도달하면 미끄러지지 않기 때문에, 단순하게 a-b를 구한 값에 v를 나눠도 정답이 안나옴

a만큼 올랏다가 b 만큼 미끄러지는 것을 반복하기 때문에, 'a-b'를 n 만큼 반복하고 마지막 날에는 a만큼 올라가고 미끄러 지지 않는다. 그래서 총 'v-b' 만큼 올라가야 한다.

`v-b = (a-b)*n` -> `n = (v-b)/(a-b)`

위의 식으로 구한 n이 소수일 경우, 소수점 이하는 day로 보면 하루가 걸린 것이기 때문에 올림의 기능을 하는 `ceil()` 사용. 

> 시간 초과를 고려하지 않았을 때

```python
a, b, v = map(int,input().split())
day = 0
height = 0

while True:
    day += 1
    height += a
    if height == v:
        print(day)
        break
    height -=b
```