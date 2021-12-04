---
title:  "[최단경로] 미래도시"
excerpt: "난이도 ★★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-12-05
last_modified_at: 2021-12-05
---

# [최단경로] 미래도시

- 문제

<br>


<br>

<hr>

<br>

<details>
<summary>정답</summary>
<div markdown="1">
<br>

```python
INF = int(1e9)

# 노드 개수 및 간선 개수
n, m = int(input().split())

# 2차원 리스트(그래프) 만들고 모든 값 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 현재 노드에서 현재 노ㄷ로 가는 비용 0으로 초기화
for a in range(1,n+1):
  for b in range(1, n+1):
    if a ==b:
      graph[a][b] = 0

# 각 간선에 대한 정보 입력 받고, 해당 값으로 초기화
for _ in range(m):
  # A와 B가 서로에게 가는 비용은 1이라고 설정
  # 문제에서 '특정 회사와 다른 회사가 도로로 연결되어 있다면 정확히 1만큼의 시간으로 이동할 수 있다.' 라는 문구가 있기 때문에
  a, b = map(int, input().split())
  graph[a][b] = 1
  graph[b]][a] = 1

# 거쳐갈 노드 x와 최종목적지 k 입력 받기
x, k = map(int, input().split())

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n+1):
  for a in range(1, n+1):
    for b in range(1, n+1):
      graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행 된 결과 출력
distance = graph[1][k] + graph[k][x]

print()
```

</div>
</details>

<br>

<details>
<summary>다른 풀이</summary>
<div markdown="1">
<br>

```python
n, m = map(int, input().split())
INF = int(1e9)
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 현재 노드에서 현재 노드로 가는 비용 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

for _ in range(m):
    # a->b, 비용은 1
    a, b = map(int, input().split())
    graph[a][b] = 1
# 1번 -> K -> X로 가는 최단경로
x, k = map(int, input().split())
start = 1

for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])
            graph[b][a] = graph[a][b]  # 양방향이므로 행,열 바꾼 값도 동일함

if graph[start][k] == INF or graph[k][x] == INF:
    print(-1)
else:
    res = graph[start][k] + graph[k][x]
    print(res)
```

</div>
</details>