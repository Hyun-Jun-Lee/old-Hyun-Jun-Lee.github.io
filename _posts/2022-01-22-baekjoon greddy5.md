---
title:  "[Greedy] 13305번 주유소"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-22
last_modified_at: 2022-01-22
---

# [Greedy] 13305번 주유소

> 문제

![image](https://user-images.githubusercontent.com/76996686/150641625-93e1655e-0489-4018-8668-5be2fb0498d6.png)


> 입력

표준 입력으로 다음 정보가 주어진다. 첫 번째 줄에는 도시의 개수를 나타내는 정수 N(2 ≤ N ≤ 100,000)이 주어진다. 다음 줄에는 인접한 두 도시를 연결하는 도로의 길이가 제일 왼쪽 도로부터 N-1개의 자연수로 주어진다. 다음 줄에는 주유소의 리터당 가격이 제일 왼쪽 도시부터 순서대로 N개의 자연수로 주어진다. 제일 왼쪽 도시부터 제일 오른쪽 도시까지의 거리는 1이상 1,000,000,000 이하의 자연수이다. 리터당 가격은 1 이상 1,000,000,000 이하의 자연수이다. 

> 출력

표준 출력으로 제일 왼쪽 도시에서 제일 오른쪽 도시로 가는 최소 비용을 출력한다. 

> 예제 입력

```
4
2 3 1
5 2 4 1
```

> 예제 출력

18

<br>

> 풀이

```python
n = int(input())

km = list(map(int,input().split()))
oil_price = list(map(int,input().split()))

# 첫 도시는 무지껀 기름 채워야함
cost = oil_price[0] * km[0]
# 현재 가장 싼 주유가격
chepest = oil_price[0]
# 지금까지 온 거리
dist = 0

for i in range(1, n-1):
    # 지금까지 주유 가격보다 이번 도시에서 주유가격이 더 싸면
    if oil_price[i]<chepest:
        # 가장 싼 주유가격 * 지금까지 온 거리
        cost += chepest * dist
        # 지금까지 온 거리 및 가장 싼 주유가격 갱신
        dist = km[i]
        chepest = oil_price[i]
    else:
        dist += km[i]
    # 마지막 도로 계산
    if i == n-2:
        cost += chepest * dist

print(cost)
```

- for문을 통해 현재 주유 가격보다 더 싼 가격이 나오면 갱신하면서 풀어가기