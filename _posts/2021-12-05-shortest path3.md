---
title:  "[최단경로] 전보"
excerpt: "난이도 ★★"

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-12-05
last_modified_at: 2021-12-05
---

# [최단경로] 전보

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
import heapq

# 무한을 의미하는 값 10억
INF = int(1e9)

# 노드 개수, 간선 개수 입력받기
n, m = map(int,input().split())

# 시작 노드 번호 입력 받기
start = int(input())

# 각 노드에 연결되있는 노드 정보 담는 리스트
graph = [[] for i in range(n+1)]

# 최단 거리 테이블 무한으로 초기화
distance = [INF] * (n+1)

# 간선 정보 입력 받기
for _ in range(m):
  a, b, c = map(int,input().split())
  # a번 노드에서 b번 노드로 가는 비용이 c라는 뜻
  graph[a].append((b,c))

def dijkstra(start):
  q = []
  # 시작 노드로 가기 위한 최단 경로 0으로 설정 후 큐에 삽입
  heapq.heappush(q,(0,start))
  # 시작 노드 초기화
  distance[start] = 0
  while q: # 큐가 비어있지 않다면
    # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
    dist, now = heapq.heappop(q)
    # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
    if distance[now] < dist:
      continue
    # 현재 노드와 연결된 다른 인접 노드 확인
    for i in graph[now]:
      cost = dist + i[1]
      # 현재 노드 거쳐 다른 노드로 이동하는 거리가 더 짧은 경우
      if cost < distance[i[0]]:
        distance[i[0]] = cost
        heapq.heappush(q, (cost,i[0]))


# 다익스트라 알고리즘 수행
dijkstra(start)

# 도달할 수 있는 노드 개수
count = 0
# 도달할 수 있는 노드 중 가장 멀리 있는 노드와의 최단 거리
max_distance = 0

# 모든 노드로 가기 위한 최단 거리 출력
for d in distance:
  # 도달할 수 없는 경우, 무한이라고 출력
  if d != INF:
    count += 1
    max_distance = max(max_distance, d)

# 시작 노드 제외해야 하기 때문에 count -1
print(count-1, max_distance)
```

</div>
</details>

<br>

<details>
<summary>다른 풀이</summary>
<div markdown="1">
<br>

```python
import heapq

n, m, c = map(int, input().split())
INF = 1001
distance = [INF] * (n+1)
graph = [[] for _ in range(n+1)]
for _ in range(m):
    x, y, z = map(int, input().split())
    graph[x].append((y, z))
# 시작노드(c) 처리
q = []
distance[c] = 0
heapq.heappush(q, (0, c))
while q:
    dist, node = heapq.heappop(q)
    if dist > distance[node]:
        continue
    for next in graph[node]:
        cost = distance[node] + next[1]
        if cost < distance[next[0]]:
            distance[next[0]] = cost
            heapq.heappush(q, (cost, next[0]))

count = 0
max_dist = -1
for i in range(1, n+1):
    if distance[i] == 0 or distance[i] == INF:
        continue
    count += 1
    max_dist = max(max_dist, distance[i])

print(count, max_dist)
```

</div>
</details>