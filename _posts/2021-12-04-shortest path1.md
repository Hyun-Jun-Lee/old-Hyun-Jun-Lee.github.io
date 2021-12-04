---
title:  "[최단경로] 다익스트라 알고리즘, 플로이드워셜 알고리즘"
excerpt: ""

categories:
- Algorithm

toc: false
toc_sticky: false

date: 2021-12-05
last_modified_at: 2021-12-05
---

# 1. 간단한 다익스트라 알고리즘

시간 복잡도 : O(V^2), 총 O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 탐색해야 하고, 현재 노드와 연결된 노드를 일일이 확인해야 하기 때문에!

전체 노드의 개수가 5,000개 이하라면 해당 코드 사용 

```python
# 무한을 의미하는 값 10억
INF = int(1e9)

# 노드 개수, 간선 개수 입력받기
n, m = map(int,input().split())

# 시작 노드 번호 입력 받기
start = int(input())

# 각 노드에 연결되있는 노드 정보 담는 리스트
graph = [[] for i in range(n+1)]

# 방문한 적 있는지 체크하는 리스트
visited = [False] * (n+1)

# 최단 거리 테이블 무한으로 초기화
distance = [INF] * (n+1)

# 간선 정보 입력 받기
for _ in range(m):
  a, b, c = map(int,input().split())
  # a번 노드에서 b번 노드로 가는 비용이 c라는 뜻
  graph[a].append((b,c))

# 방문하지 않는 노드 중, 최단 거리가 짧은 노드의 번호 반환
def get_smallest_node():
  min_value = INF
  # 가장 거리가 짧은 노드(인덱스)
  index = 0
  for i in range(1,n+1):
    # 최단 거리가 min_value보다 작고 아직 방문하지 않앗다면 교체
    if distance[i] < min_value and not visited[i]:
      min_value = distance[i]
      index = i
  return index

def dijkstra(start):
  # 시작 노드 초기화
  distance[start] = 0
  visited[start] = True
  for j in graph[start]:
    distance[j[0]] = j[1]
  # 시작 노드를 제외한 전체 n-1 개의 노드에 대해 반복
  for i in range(n-1):
    # 현재 최단 거리가 가장 짧은 노드 방문 처리
    now = get_smallest_node()
    visited[now] = True
    # 현재 노드와 연결된 다른 노드 확인
    for j in graph[now]:
      cost = distance[now] + j[1]
      # 현재 노드를 거쳐 다른 노드로 가는 거리가 더 짧은 경우
      if cost < distance[j[0]]:
        distance[j[0]] = cost

# 다익스트라 알고리즘 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우, 무한이라고 출력
  if distance[i] == INF:
    print("INF")
  # 도달할 수 있는 경우 거리 출력
  else:
    print(distance[i])
```

<br>

# 2. 개선된 다익스트라 알고리즘

이 방법은 최악의 경우에도 O(ElogV) 보장, V는 노드의 개수이고 E는 간선의 개수
개선된 다익스트라 알고리즘은 Heap 구조 사용, 최단 거리에 대한 정보를 Heap에 담아서 처리하므로 더 빠르게 찾을 수 있음

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

# 모든 노드로 가기 위한 최단 거리 출력
for i in range(1, n+1):
  # 도달할 수 없는 경우, 무한이라고 출력
  if distance[i] == INF:
    print("INF")
  # 도달할 수 있는 경우 거리 출력
  else:
    print(distance[i])
```

# 3. 플로이드 워셜 알고리즘

시간복잡도 : O(N^3)

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
  # A에서 B로 가는 비용은 C라고 설정
  a, b, c = map(int, input().split())
  graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n+1):
  for a in range(1, n+1):
    for b in range(1, n+1):
      graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행 된 결과 출력
for a in range(1, n+1):
  for b in range(1, n+1):
    # 도달할 수 없는 경우 무한 출력
    if graph[a][b] == INF:
      print('INF')
    else:
      print(graph[a][b], end = "")

print()
```