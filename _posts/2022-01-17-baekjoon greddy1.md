---
title:  "[Greedy] 11047번 동전 0"
excerpt: "Baekjoon 단계별 문제"

categories:
- BAEKJOON

toc: True
toc_sticky: True

date: 2022-01-17
last_modified_at: 2022-01-17
---

# [Greedy] 11047번 동전 0

> 문제

준규가 가지고 있는 동전은 총 N종류이고, 각각의 동전을 매우 많이 가지고 있다.

동전을 적절히 사용해서 그 가치의 합을 K로 만들려고 한다. 이때 필요한 동전 개수의 최솟값을 구하는 프로그램을 작성하시오.

> 입력

첫째 줄에 N과 K가 주어진다. (1 ≤ N ≤ 10, 1 ≤ K ≤ 100,000,000)

둘째 줄부터 N개의 줄에 동전의 가치 Ai가 오름차순으로 주어진다. (1 ≤ Ai ≤ 1,000,000, A1 = 1, i ≥ 2인 경우에 Ai는 Ai-1의 배수)

> 출력

첫째 줄에 K원을 만드는데 필요한 동전 개수의 최솟값을 출력한다.

> 예제 입력

10 4200
1
5
10
50
100
500
1000
5000
10000
50000

> 예제 출력

6

<br>

> 풀이

```python
n, k = map(int,input().split())
coin_list = []
cnt = 0
for i in range(n):
    coin = int(input())
    coin_list.append(coin)

coin_list.sort(reverse=True)

for i in coin_list:
    if k==0:
        break
    # 쓰인 동전 수
    cnt += k//i
    k %= i

print(cnt)
```

- `/` : 나누기, 10/3 = 3.3333
- `//` : 몫 구하기, 10//3 = 3
- `%` : 나머지 구하기, 10%3 = 1

```python
for i in coin_list:
    # 쓰인 동전 수
    cnt += k//i
    k %= i
```

4200%50000 = 4200
    ...
4200%1000 = 200 (cnt=4, k=200)
200%500 = 200 (cnt=4, k=200)
200%100 = 0 (cnt=6, k=0)

> 다른 풀이

```python
n, k = map(int, input().split())
m = []
num = 0
for i in range(n):
    m.append(int(input()))
# 역방향으로 for문
for i in range(n - 1, -1, -1):
    if k == 0:
        break
    # coin이 k보다 크면 pass
    if m[i] > k:
        continue
    num += k // m[i]
    k %= m[i]
print(num)
```